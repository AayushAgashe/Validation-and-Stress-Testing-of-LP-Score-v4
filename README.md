# LP Score v4 — Validation & Stress Test

This repository contains the analysis, code, and findings for validating and stress-testing the **Liquidity Provider (LP) Score v4** system.

## Project Overview

The dataset assigns each wallet an `aggregated_lp_score`, category-level fields, and multiple per-pool scores with detailed breakdowns. However, the aggregated score does not directly match the sum of pool scores or category breakdowns, suggesting hidden weighting, normalization, or adjustment.

The objective of this project is to:
- Validate how the aggregated score is computed.
- Check whether scores align with wallet activity (deposits, retention, volatility).
- Verify internal consistency across scoring components.
- Identify anomalies and outliers in scoring behavior.

## Key Findings

1. Aggregated scores never equal raw pool score sums (0% exact matches).
2. A linear adjustment exists: `agg ≈ 0.18 × pool_sum + 161` (weak fit, R² = 0.40).
3. Normalization by pool count gives stronger correlation (0.965).
4. Category breakdown fields act as diagnostics, not subscores.
5. Higher deposits generally lead to higher scores, but zero-deposit wallets still score nonzero.
6. Strongest drivers of pool scores: withdraw volume, holding time, liquidity retention, deposit volume.
7. Deposit frequency shows a negative effect.
8. About 15% of wallets are anomalous (e.g., zero deposits with positive scores, inflated score-to-deposit ratios).

## Deliverables
- **Code**: Reproducible notebook for validation and analysis.
- **Anomalies CSV**: Wallet IDs with anomalous behavior, metrics, and ratios.

