---
slug: model-freshness
aliases:
- model freshness
- model staleness
- stale model
- stale checkpoint
- checkpoint staleness
- checkpoint age
- embedding freshness
- embedding staleness
- feature freshness
- feature staleness
- staleness tradeoff
- online training
- online streaming training
- streaming training
- real-time training
- realtime training
- incremental learning
- incremental training
- incremental update
- online update
- delta update
- model retraining
- retraining frequency
- retraining cadence
- retrain frequency
- parameter synchronization
- concept drift
---

## What it is

How quickly a deployed recommender absorbs new interactions: retraining cadence, incremental / online / streaming training, parameter synchronization to serving, and the measured cost of model, embedding, or feature staleness.

## Papers

- [[2108.13299]] Incremental Learning for Personalized Recommender Systems (Linkedin, 2021)
- [[2209.07663]] Monolith: Real Time Recommendation System With Collisionless Embedding Table (Bytedance, 2022)
- [[2210.08804]] A GPU-specialized Inference Parameter Server for Large-Scale Deep Recommendation Models (Nvidia, 2022)
- [[2306.00248]] TransAct: Transformer-based Realtime User Action Model for Recommendation at Pinterest (Pinterest, 2023)
- [[2410.06497]] ERCache: An Efficient and Reliable Caching Framework for Large-Scale
  User Representations in Meta's Ads System (Meta, 2024)
- [[2410.18111]] Data Efficiency for Large Recommendation Models (Google, 2024)
- [[2502.10514]] Applying Deep Learning to Ads Conversion Prediction in Last Mile Delivery Marketplace (Doordash, 2025)
- [[2505.02844]] Feature Staleness Aware Incremental Learning for CTR Prediction (Tencent, 2025)
- [[2505.18897]] Improving Ad matching via Cluster-Adaptive Keyword Expansion and Relevance tuning (Ebay, 2025)
- [[2508.11977]] TBGRecall: A Generative Retrieval Model for E-commerce Recommendation Scenarios (Alibaba-inc, 2025)
- [[2510.13405]] Optimizing Storage Overhead of User Behavior Log for ML-embedded Mobile Apps (Bytedance, 2025)
- [[2512.12295]] Near-Zero-Overhead Freshness for Recommendation Systems via Inference-Side Model Updates (Bytedance, 2025)
- [[2601.20307]] Delayed Feedback Modeling for Post-Click Gross Merchandise Volume Prediction: Benchmark, Insights and Approaches (Alibaba-inc, 2026)
- [[2602.08678]] SA-CAISR: Stage-Adaptive and Conflict-Aware Incremental Sequential Recommendation (Tencent, 2026)
- [[2602.17050]] Multi-Probe Zero Collision Hash (MPZCH): Mitigating Embedding Collisions and Enhancing Model Freshness in Large-Scale Recommenders (Meta, 2026)
- [[2604.08933]] IAT: Instance-As-Token Compression for Historical User Sequence Modeling in Industrial Recommender Systems (Bytedance, 2026)
- [[2604.26247]] TimeMM: Time-as-Operator Spectral Filtering for Dynamic Multimodal Recommendation (Xiaohongshu, 2026)
- [[2605.00324]] Intelligent Elastic Feature Fading: Enabling Model Retrain-Free Feature Efficiency Rollouts at Scale (Meta, 2026)
- [[2605.29755]] Rec-Distill: An Industrial Distillation Pipeline for Large-Scale Recommendation Models (Bytedance, 2026)
- [[2607.14331]] Long-History User Transformers for Real-Time Ad Ranking (Yandex, 2026)
- [[2607.15242]] Mutable Low-Rank Sketches for Retrain-Free Recommendation (Criteo, 2026)
- [[2607.24092]] ConAlign: Conditional Alignment Framework for Balancing Biased and Unbiased Recommendation (Kuaishou, 2026)
- [[2607.25110]] Memory Layer: Train the In-Model Cache for Recommendation Models (Meta, 2026)
- [[2609.16407]] Balancing Trial and Reorder: A Hybrid Sequential Transformer-GBDT Ranker for On-Demand Delivery (Wolt, DoorDash, 2026)
