# recsys-kb

Versioned knowledge base of recent **industry** recommendation-systems papers, built from the
GitHub-issue feed produced by [`arxiv_rec_finder`](https://github.com/zippeurfou/arxiv_rec_finder).

This is a **data repo** (Markdown + JSONL + YAML). The Python builder that populates it lives in
`arxiv_rec_finder` (`kb/` package). It is consumed by a global OpenCode skill
(`recsys-industry-kb`) as a grounding layer for recsys ML-engineering work.

Design & implementation plan: see `arxiv_rec_finder/docs/plans/2026-07-01-recsys-industry-kb-*.md`.

## Layout

```
index.jsonl            # 1 line/paper: id, title, year, companies, concepts[], url, issue#
papers/<arxiv_id>.md   # per-paper note (see schema below)
concepts/<slug>.md     # per canonical concept; intro + machine-generated backlinks
vocabulary.yaml        # canonical concept slug <-> aliases (edit + re-canonicalize to re-tag)
unmapped_concepts.md   # generated: raw concepts with no canonical mapping, ranked by frequency
state.json             # last-built issue number/date, for incremental refresh
```

Full-text markdown is **not** stored here — it is re-derivable from the arXiv id and cached
locally (gitignored, e.g. `~/.cache/recsys-kb/fulltext/`).

## Paper note schema (`papers/<arxiv_id>.md`)

```markdown
---
arxiv_id: <id>
title: "<title>"
year: <int>
companies: [<company>, ...]
url: <arxiv url>
issue: <github issue number>
concepts_raw: [<verbatim techniques the paper discusses; vocabulary-INDEPENDENT>]
concepts: [<canonical slugs derived from concepts_raw via vocabulary.yaml>]
citation_count: <int|null>   # Semantic Scholar, best-effort
last_built: <YYYY-MM-DD>
---

## Summary
## Technical note      # problem / method / result, from full text
## References          # title (+ arxiv id/doi when resolvable) -> enables citation traversal
```

`concepts_raw` is the expensive, read-once, vocabulary-independent record of what the paper
actually discusses. `concepts` is cheap and re-derivable: change `vocabulary.yaml`, re-run
`--canonicalize`, and every paper is re-tagged with no re-reading.

## Refresh (ongoing — a few new papers)

Extraction is **agent-driven** (an LLM agent reads each new paper). Use the
`recsys-industry-kb` OpenCode skill, or run the loop manually:

```bash
git pull
# 1) fetch + cache full text for new papers (no LLM)
uv run --project ~/Projects/arxiv_rec_finder python -m kb.build \
    --kb-dir ~/Projects/recsys-kb prepare --repo zippeurfou/arxiv_rec_finder --incremental
# 2) AGENT reads .pending.jsonl -> writes .extractions.jsonl  (arxiv_id, concepts_raw, technical_note)
# 3) build notes + index, then commit
uv run --project ~/Projects/arxiv_rec_finder python -m kb.build \
    --kb-dir ~/Projects/recsys-kb ingest --extractions ~/Projects/recsys-kb/.extractions.jsonl
git push
```

## Backfill (one-time, batched, resumable)

Same loop with `--limit N` per batch; the `state.json` watermark advances on each
`ingest`, so batches march through the corpus (oldest issue first) without skipping.
Repeat until `prepare` reports `prepared=0`. For a batch, split `.pending.jsonl`
across parallel extraction subagents (each writing its own file), concatenate, then
`ingest`.

```bash
uv run --project ~/Projects/arxiv_rec_finder python -m kb.build \
    --kb-dir ~/Projects/recsys-kb prepare --repo zippeurfou/arxiv_rec_finder --incremental --limit 40
# ... agent extraction -> .extractions.jsonl ...
uv run --project ~/Projects/arxiv_rec_finder python -m kb.build \
    --kb-dir ~/Projects/recsys-kb ingest --extractions ~/Projects/recsys-kb/.extractions.jsonl
```

Retry papers that had no usable full text (recorded in `state.json.failures`):
`... prepare --retry-failed` then extract + ingest.

**Progress:** ~38 papers ingested (watermark at issue 40); ~2,415 remain.

