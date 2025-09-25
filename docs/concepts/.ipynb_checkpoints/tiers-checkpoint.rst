.. _concepts-tiers:

Tiers 1-3
=====================

Tier-0: Lexical / Heuristic
---------------------------
Lightweight word-maps or rules. Useful for bootstrapping and baseline robustness.
Deterministic but limited generalization.

Tier-1: SBERT Latents + Deterministic Rails
-------------------------------------------
Mapper operates in **clean SBERT latent space**. NGF rails enforce deterministic
routing and verification. Strong performance on curated primitives (ARC/DeFi).

Tier-2: WDD on SBERT (Warp–Detect–Denoise)
------------------------------------------
WDD applied to SBERT latents for **separation** and **stability**. Improves
perturbation robustness and reduces false positives; abstains remain principled.

Tier-3: LLM Latents Sidecar (Planned)
-------------------------------------
Swap SBERT for **LLM-derived latents** while retaining NGF rails for determinism.
Objective: expand coverage without sacrificing abstain guarantees.

Choosing a Tier
---------------
- Start **Tier-1** for quick wins and deterministic baselines.
- Move to **Tier-2** when robustness under perturbation matters.
- Graduate to **Tier-3** to broaden capability once rails/verifiers are mature.
