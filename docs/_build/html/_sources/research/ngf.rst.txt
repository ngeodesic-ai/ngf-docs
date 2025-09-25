.. _research-ngf:

Noetic Geodesic Framework
=========================================

Overview
--------
The **Noetic Geodesic Framework (NGF)** is a geometric approach to deterministic AI
reasoning. It reframes reasoning over **latent spaces** as geodesic traversals through
**warped manifolds**, where semantic structure is enforced by energy wells. This lets
us suppress hallucinations and enforce **stable, truth‑aligned reasoning** by shaping
the geometry that models traverse.

NGF operates at the *embedding* level, not the text level; it is pluggable into
LLMs and encoders by intercepting and shaping their latent trajectories.

.. admonition:: Key Idea
   :class: tip

   Instead of fine‑tuning weights or prompt engineering, **NGF shapes the latent
   manifold** so that trajectories follow **deterministic geodesics** toward
   correct regions (semantic wells), and away from noise.

Origins & Motivation
--------------------
- **Problem:** Large models excel at pattern completion but can be *stochastically
  brittle* and hallucinate under distribution shift, weak calibration, or noisy
  contexts.
- **Hypothesis:** If we can restructure the latent manifold so that task‑relevant
  regions form **stable wells** separated by margins, then short, deterministic
  geodesics emerge—yielding **reproducible** decisions.
- **Evidence path (ngf‑alpha):** A staged research plan progressed from toy
  spaces :math:`\mathbb{R}^4`/ :math:`\mathbb{R}^9` to noisy external latents
  (LLM hidden states), culminating in **Stage‑11** where **Warp → Detect → Denoise**
  became a working doctrine and delivered robustness gains on benchmarks.

Warp / Detect / Denoise (WDD)
-----------------------------
**WDD** is NGF’s core doctrine for stabilizing latent trajectories.

1) **Warp**  
   Map raw latents to a geometry where task structure is explicit—e.g., by
   projecting, aligning, and **warping into dominant semantic wells** so that
   correct routes shorten and foils lengthen.

2) **Detect**  
   Apply calibrated matched‑filters (with nulls/foils) to **separate signal from
   off‑manifold noise**. This step routes traces toward viable candidates and
   away from ambiguous regions, preserving plausible options while filtering out
   mismatches.

3) **Denoise**  
   Reduce residual noise and **increase margins** via temporal smoothing (EMA,
   median), phantom guards, jitter averaging, and related filters. The result is
   improved **reproducibility** under prompt/context perturbations and better
   calibration of confidence.

Trace Manifold Shaping
----------------------
NGF treats reasoning as **geodesic motion** on a shaped manifold:

- **Semantic wells**: regions where class/task affinity concentrates; warp
  deepens the correct well and flattens distractions.
- **Geodesic nudges**: gentle geometric biases (not weight changes) steer
  trajectories into the right wells without overfitting the model.
- **Separation & margins**: detection and denoising enlarge the gap between
  correct vs. foil routes, yielding **deterministic traces**.
- **Abstain as geometry**: when detection reveals ambiguity (overlapping wells,
  weak margins), the system **ABSTAINS** rather than hallucinating.

Practical Implications
----------------------
- **Plug‑in module:** NGF can sit beside any embedding‑producing model (LLMs,
  encoders, diffusion models) without retraining the base model.
- **Deterministic sidecars:** This is the foundation for **Micro‑LMs**—domain‑
  specialized, auditable sidecars that map NL intent → primitives under strict
  verifiers and **explicit abstains**.
- **Safety & audit:** Determinism + abstain logic produce **replayable traces**
  suitable for regulated domains (finance, healthcare, defense).

Pointers & Further Reading
--------------------------
- **ngf‑alpha (research log & stages)** — staged experiments from toy spaces to
  LLM latents; **Stage‑11** establishes the WDD doctrine and reports robustness
  gains on ARC‑like and HellaSwag‑style tests.
- **Patents (non‑provisional)** — filings covering WDD, Micro‑LM sidecars,
  trace shaping, and abstain logic.
- **Technical paper (work in progress)** — NGF: Deterministic AI via Warped
  Manifolds; early preprint and article draft referenced in the repository.

