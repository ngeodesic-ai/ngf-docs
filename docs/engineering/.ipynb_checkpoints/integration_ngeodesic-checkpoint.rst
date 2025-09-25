.. _engineering-integration-ngeodesic:

Integration with ngeodesic
==========================

Overview
--------
The **micro-lm** product line is built on top of the **ngeodesic** Python package,
which implements the **Noetic Geodesic Framework (NGF)** rails.

This integration ensures that Micro‑LMs inherit deterministic behavior,
WDD doctrine, and abstain guarantees from NGF.

How Integration Works
---------------------
- **ngf-alpha (research):** proved Warp → Detect → Denoise (WDD) in staged experiments.  
- **ngeodesic (framework):** packaged NGF rails (Stage‑11) into a stable API.  
- **micro-lm (applications):** consumes ngeodesic APIs to run domain‑specific sidecars.  

Rails Integration
-----------------
- Micro‑LMs call ``ngeodesic.core`` modules for warp, detect, and denoise.  
- Stage‑11 parser runs latent traces through:  
  - **Warp:** PCA projection + funnel shaping.  
  - **Detect:** matched filters + nulls/foils.  
  - **Denoise:** hybrid EMA/median + jitter averaging.  
- Deterministic traces and abstains are returned to the Micro‑LM harness.

Tier-2 Refactor
---------------
In Tier‑2, Micro‑LMs expanded to use **auditors** powered by ngeodesic WDD rails:

- Mapper proposes candidate primitive.  
- Auditor projects into PCA space, applies WDD detection, checks nulls/foils.  
- Auditor may **abstain**, even if mapper proposed a label.  
- Prevents tautology by keeping mapper vs audit paths independent. 【231†TIER2.md】

Policy & Verifiers
------------------
- After ngeodesic rails return candidates, Micro‑LMs apply **policy checks**.  
- Example (DeFi): enforce Loan‑to‑Value (LTV), Health Factor (HF), oracle freshness.  
- Example (ARC): enforce schema compliance, sanity checks on transformations.  
- This layered design means:  
  - **ngeodesic rails** ensure determinism.  
  - **Micro‑LM policy/verifiers** ensure domain‑specific safety.

Benefits
--------
- **Reuse:** Rails logic is maintained in ngeodesic, keeping micro-lm lightweight.  
- **Stability:** Shared rails ensure consistent behavior across domains.  
- **Separation of concerns:** Research (ngf-alpha) → framework (ngeodesic) → product (micro-lm).  

