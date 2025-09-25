.. _research-ngf-alpha-experiments:

NGF-Alpha Experiments
=====================

Overview
--------
**ngf-alpha** was the first research repository for exploring the **Noetic Geodesic
Framework (NGF)**. It documented staged experiments that tested whether latent
manifolds could be warped, detected, and denoised to produce **deterministic,
reproducible reasoning**.

The staged design allowed systematic exploration from toy settings to real latent
spaces, gradually validating the Warp–Detect–Denoise (WDD) doctrine.

Early Prototypes
----------------
- **Stage 0–3 (Toy Spaces):**
  - Operated in simple vector spaces (:math:`\mathbb{R}^4`, :math:`\mathbb{R}^9`).
  - Tested geodesic shaping in low dimensions.
  - Showed that introducing *semantic wells* could reduce trajectory variance.

- **Stage 4–6 (Synthetic Trace Families):**
  - Applied WDD logic to synthetic ARC‑like traces.
  - Proved that matched filters with nulls/foils could separate valid routes
    from noise.
  - Early use of temporal smoothing to reduce decision instability.

- **Stage 7–9 (Noisy External Latents):**
  - Integrated SBERT embeddings and LLM hidden states.
  - Demonstrated that warp alignment + detection thresholds could **stabilize**
    mappings from NL prompts → task primitives.

- **Stage 10–11 (Full NGF Rails):**
  - Introduced the canonical Warp → Detect → Denoise sequence.
  - Benchmarked robustness under perturbations (synonyms, paraphrases, jitter).
  - Validated **abstain logic** as a principled alternative to misclassification.

Key Results → Micro-LMs
-----------------------
1. **WDD Works in Practice**  
   The staged experiments confirmed that WDD reliably improved reproducibility,
   separation, and robustness. This validated NGF as more than theory—it was
   a working framework.

2. **Deterministic Traces**  
   By Stage‑11, identical prompts produced **identical traces and outcomes**
   across runs, a property absent in baseline models.

3. **Principled Abstains**  
   Experiments showed that ambiguity could be detected geometrically—when wells
   overlapped or margins were thin, abstains were triggered instead of guesses.

4. **Blueprint for Sidecars**  
   The insights from ngf‑alpha directly inspired **Micro‑LMs**: lightweight,
   domain‑specific reasoning sidecars that use NGF rails to map intent to
   primitives under verifiers.

   - **ARC Micro‑LM** became the reasoning stress test.  
   - **DeFi Micro‑LM** became the production‑style demo with policy checks.

Pointers & Further Reading
--------------------------
- See the `ngf-alpha` repository for full experimental logs and staged designs.  
- Stage‑11 experiments are particularly important: they introduced canonical
  WDD rails and proved abstain determinism.  
- For patent coverage, see **Warp–Detect–Denoise**, **Micro‑LM sidecars**, and
  **trace manifold shaping** filings.  
