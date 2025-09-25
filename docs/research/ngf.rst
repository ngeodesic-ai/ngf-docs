.. _research-ngf:

Noetic Geodesic Framework (Alpha)
=================================

🚀 **The Noetic Geodesic Framework (NGF)** is a geometric approach to deterministic AI reasoning.  
It reframes reasoning in latent space as geodesic traversals through warped manifolds, where semantic structure is enforced by energy wells.  
This allows us to suppress hallucinations and enforce stable, truth-aligned reasoning.

NGF builds on two key pillars:

- **Latent Vector Embeddings** — high-dimensional representations (used across modern AI, including LLMs).
- **Warp → Detect → Denoise Doctrine (Stage 11)** — our pipeline that shapes these embeddings into deterministic geodesic trajectories.

LLMs vs Vector Embeddings
-------------------------

- **LLMs (Large Language Models):** Sequence models that operate on tokens, typically built on transformer architectures.  
  They internally rely on vector embeddings (hidden states) but expose only the text interface.
- **Vector Embeddings:** High-dimensional vectors that encode semantic meaning.  
  These can be obtained independently of an LLM (e.g., sentence embeddings, ARC synthetic embeddings) and are directly manipulable.

**NGF operates at the embedding level**, not at the text level.  
This means NGF methods are pluggable into any LLM or embedding model.  
Instead of manipulating prompts or fine-tuning weights, NGF directly reshapes latent trajectories in vector space.

Research Plan Stages
--------------------

The NGF follows a 12-step research plan, with 10 completed stages posted here where step 10 marked the public rollout.  
Steps 11–12 (milestone reports) are in progress.

+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| Stage | Description                                   | Level               | Hardware    | Folder/Code                 |
+=======+===============================================+=====================+=============+=============================+
| 1     | Toy Example                                   | Embedding / toy R⁴  | CPU         | toy-example/                |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 2     | Embed Grid Intelligently                      | Embedding / toy R⁴  | CPU         | embed-grid/                 |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 3     | Rotation Matrix Integration                   | Embedding / toy R⁴  | CPU         | rotation-matrix/            |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 4     | Simulate Pattern Completion                   | Embedding / toy R⁴  | CPU         | pattern-completion/         |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 5     | Higher-Dim Embeddings                         | Embedding / toy R⁹  | CPU         | higher-dim-embeddings/      |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 6     | Integrate Dynamic Intelligence                | Embedding / toy R⁹  | CPU         | dynamic-intelligence/       |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 7     | ARC Question                                  | Embedding / toy R⁹  | CPU         | rudimentary-arc/            |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 8     | LLM Latent Embedding                          | Embedding / external| CPU         | llm-latent-embedding/       |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 9     | Warp LLM Interference                         | Embedding / external| CPU         | warp-interference/          |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 10    | Rudimentary Benchmarks                        | Embedding / external| CPU         | rudimentary-interference/   |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 11    | Small Benchmarks                              | Latent / LLM        | CPU         | small-benchmarks/           |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+
| 12    | Large Benchmark (coming)                      | Latent / LLM        | A100/T4     | milestone-benchmark/        |
+-------+-----------------------------------------------+---------------------+-------------+-----------------------------+


Summary Note
------------

Stages 1–10 were critical as they provided the evidence that warping is effective.  
In toy R⁴ and R⁹ spaces we saw clean, causal effects; in external LLM embeddings we validated that the same principles held under noise and larger dimensions.  

Without this scaffolding, we would not have had the evidence to help cut through Stage 11 when the messy latents looked bleak.  
If we apply the engine analogy: Stages 1–7 were toy engines, Stages 8–10 were mock-ups, and Stage 11 was where we dropped NGF into the engine bay (a live LLM).  
Stage 11 transformed that conviction into the working doctrine: **Warp → Detect → Denoise**.

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

