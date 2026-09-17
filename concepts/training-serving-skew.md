---
slug: training-serving-skew
aliases:
- training serving skew
- train serve skew
- train/serve skew
- training/serving skew
- training serving consistency
- training serving alignment
- training serving discrepancy
- training serving inconsistency
- training inference discrepancy
- online offline gap
- offline online gap
- offline online metric gap
- online offline discrepancy
- offline online discrepancy
- online offline inconsistency
- offline online consistency
- online offline consistency
- feature logging
- logged features
- online feature logging
- feature lag
- feature join offset
- lag matched features
- point in time correctness
- point in time features
- cached residuals
---

## What it is

Differences between what a model sees in training and at serving time: feature-pipeline lag and stale feature stores, offline-joined vs served-logged features, cached residuals, and the resulting offline/online metric gaps. Remedies include lag-matched training features and logging features at serve time.

## Papers

- [[2502.10514]] Applying Deep Learning to Ads Conversion Prediction in Last Mile Delivery Marketplace (Doordash, 2025)
- [[2506.02267]] TransAct V2: Lifelong User Action Sequence Modeling on Pinterest Recommendation (Pinterest, 2025)
- [[2508.05093]] An End-to-End Multi-objective Ensemble Ranking Framework for Video Recommendation (Kuaishou, 2025)
- [[2602.11410]] CADET: Context-Conditioned Ads CTR Prediction With a Decoder-Only Transformer (Linkedin, 2026)
- [[2604.08181]] Long-Term Embeddings for Balanced Personalization (Zalando, 2026)
- [[2604.24806]] Versioned Late Materialization for Ultra-Long Sequence Training in Recommendation Systems at Scale (Meta, 2026)
- [[2605.00324]] Intelligent Elastic Feature Fading: Enabling Model Retrain-Free Feature Efficiency Rollouts at Scale (Meta, 2026)
- [[2605.11854]] Self-Distilled Trajectory-Aware Boltzmann Modeling: Bridging the Training-Inference Discrepancy in Diffusion Language Models (Huawei, 2026)
- [[2607.14331]] Long-History User Transformers for Real-Time Ad Ranking (Yandex, 2026)
- [[2607.25110]] Memory Layer: Train the In-Model Cache for Recommendation Models (Meta, 2026)
- [[2608.16872]] Impression Share Prediction: An Offline Evaluation Task for Ranking Systems (Meta, 2026)
- [[2609.16407]] Balancing Trial and Reorder: A Hybrid Sequential Transformer-GBDT Ranker for On-Demand Delivery (Wolt, DoorDash, 2026)
