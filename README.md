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

## Refresh

```bash
git pull
uv run --project ~/Projects/arxiv_rec_finder python -m kb.build \
    --incremental --repo zippeurfou/arxiv_rec_finder --kb-dir ~/Projects/recsys-kb
```
