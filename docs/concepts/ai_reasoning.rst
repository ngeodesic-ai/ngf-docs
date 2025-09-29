.. _concepts-ngf-rails:

Deterministic AI Reasoning
============================================

**NGF rails** implement the **WDD** pipeline to stabilize decisions and enforce safety.

Warp
----
LLMs spread meaning across a vast, noisy latent space. **Warping** reshapes this space into a stable
geometry — a funnel-like energy landscape where valid solutions settle naturally into a single well.
This ensures reasoning trajectories are attracted to truth-aligned basins instead of drifting.

Detect
------
Once warped, the sidecar applies **matched filtering** to separate genuine signals from noise.
Two thresholds are applied: one relative (to catch strong local wells) and one calibrated against
a null model (to reject phantoms). This lets the system PASS only when a stable solution is present.

Denoise
-------
**Denoising** suppresses spurious or unstable wells that could masquerade as answers. Control guards
are applied to prevent oscillation, collapse edge cases, and enforce consistency across reruns.
The effect is clean, reproducible reasoning with phantom wells removed.

Verify
------
Every verdict is labeled as **PASS, ABSTAIN, or REJECT** with grounded spans. This creates a replayable
audit trail: anyone can verify not just the answer, but the reasoning process that led to it.
This verification step transforms black-box LLM outputs into auditable, deterministic rails.


Design Goals
------------
- **Deterministic traces.**
- **Separation:** preserve correct routes; suppress foils.
- **Abstain when unsure:** fail-safe before execution.
