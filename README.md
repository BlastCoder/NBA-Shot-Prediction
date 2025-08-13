# NBA-Shot-Prediction

**NBA Shot Quality (xEFG) — 3-season model, out-of-time tested**

* **Goal:** Estimate shot make probability (and xEFG) from public shot-location/context, then separate **shot selection** (xEFG) from **shot-making** (actual − expected).
* **Data:** 4 seasons, **843,626** FGA (2021-22 → 2024-25). Train on **3 seasons** with time-decay weights (0.25 / 0.50 / 1.00); **held-out test = 2024-25**.
* **Features:** Distance, angle (**sin/cos**), 3PT & corner-3 flags, quarter, **time remaining**, **home/away**, plus categorical context (**SHOT\_ZONE / ZONE\_NAME / ZONE\_RANGE** and **top-20 ACTION\_TYPE** one-hots).
* **Models:** Logistic Regression (calibrated baseline) and **HistGradientBoosting**; boosted model **isotonic-calibrated** on a train-only split.
* **Results (test ’24-25):** Baseline Brier ≈ **0.2499**. **Best = 0.2247** (≈**10.1%** better), **AUC = 0.661**; reliability curves near-diagonal (well-calibrated probabilities).
* **Insights (team xEFG vs actual):** Examples — **OKC +2.8 pp**, **BOS +3.9 pp**, **MEM −3.7 pp** (shot-making relative to modeled shot quality).
* **Deliverables:** Clean pipeline (per-season CSVs), calibration plot, and full **team xEFG vs actual** table (CSV).
* **Limitations / next steps:** Public data (no tracking/defender info); add player/lineup effects, playoff flag, and bootstrap CIs for team deltas; consider out-of-fold calibration and mild hyperparam tuning.
