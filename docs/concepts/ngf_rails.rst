.. _concepts-ngf-rails:

Warp → Detect → Denoise
============================================

**NGF rails** implement the **WDD** pipeline to stabilize decisions and enforce safety.

1) Warp
-------
Align raw latents or traces into a structured manifold where task-relevant geometry
is separable (e.g., bringing related prompts closer and off-task noise farther).

2) Detect
---------
Identify signal vs. off-manifold noise. This is where routing and "keep/foil"
choices are made to preserve plausible options while filtering out mismatches.

3) Denoise
----------
Reduce residual noise to improve **reproducibility** and **margin** between classes.
This increases stability under prompt perturbations and small context changes.

4) Verify
---------
Policy-layer checks before execution. Examples:
- **DeFi:** LTV/HF thresholds, oracle freshness, slippage bounds.
- **ARC:** Operation plausibility, ambiguity reduction.

Design Goals
------------
- **Deterministic traces.**
- **Separation:** preserve correct routes; suppress foils.
- **Abstain when unsure:** fail-safe before execution.
