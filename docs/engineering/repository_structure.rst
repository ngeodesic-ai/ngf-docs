.. _engineering-repository-structure:

Repository Structure
====================

Overview
--------
The NGF ecosystem is organized into three main repositories, each with a distinct role:

1. **ngf-alpha** → research prototypes and staged experiments.  
2. **ngeodesic** → the production-ready Python package implementing NGF rails.  
3. **micro-lm** → domain-specific micro‑LM applications built on top of ngeodesic.  

This layered structure ensures a clean separation between **theory, framework, and product**.

ngf-alpha (Research)
--------------------
- Repository: https://github.com/ngeodesic-ai/ngf-alpha  
- Purpose: experimental log of the **Noetic Geodesic Framework (NGF)**.  
- Content: staged experiments from toy latent spaces to real embeddings.  
- Key contribution: crystallized the **Warp → Detect → Denoise (WDD)** doctrine.  
- Outcome: validated NGF as a viable method for deterministic reasoning.  

ngeodesic (Science)
--------------------------------------
- Repository: https://github.com/ngeodesic-ai/ngeodesic  
- Purpose: implements NGF rails in a reusable, domain‑agnostic package.  
- Key features:  
  - **Warp:** PCA projection, funnel profiles, semantic well shaping.  
  - **Detect:** matched filters, null/foil separation, margin thresholds.  
  - **Denoise:** EMA+median smoothing, phantom guards, jitter averaging.  
  - **Parser API:** stock parsers + Stage‑11 geodesic parser.  
- Provides the rails and utilities for downstream micro‑LMs.  

micro-lm (Product Line)
-------------------------------------
- Repository: https://github.com/ngeodesic-ai/micro-lm  
- Purpose: applies NGF rails to build **deterministic, domain‑specific sidecars**.  
- Domains:  
  - **DeFi Micro‑LM:** maps finance prompts → primitives with LTV/HF/oracle verifiers.  
  - **ARC Micro‑LM:** stress‑tests reasoning on grid transformations.  
- Architecture (Tier‑1) 【232†OVERVIEW.md】:  
  - **Adapters:** normalize context (JSON → schema).  
  - **Mapper:** SBERT/wordmap classifiers.  
  - **Verifier:** domain policy checks.  
  - **Planner:** expands intent into structured plans.  
  - **Harness:** runs deterministically on Stage‑11 NGF rails.  
- Tier‑2 refactor 【231†TIER2.md】: introduces WDD auditors for latent separation.

Cross-Repo Flow
---------------
1. **ngf-alpha** proves the theory (WDD rails, abstain logic).  
2. **ngeodesic** packages it as a stable Python library.  
3. **micro-lm** consumes ngeodesic to deliver applied products (ARC, DeFi).  

This flow mirrors a traditional R&D pipeline: **Research → Engineering → Product**.

