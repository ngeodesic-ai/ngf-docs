.. _research-current-threads:

Current Research
========================

Overview
--------
Research on the **Noetic Geodesic Framework (NGF)** continues beyond Tier‑1 and Tier‑2,
with active investigations into:

1. Latents: **SBERT vs LLM‑derived embeddings**.  
2. Separation of **Mapper** vs **Audit** functions.  
3. **Abstain philosophy** as a first‑class design principle.

Latents (SBERT vs LLM)
----------------------
- **SBERT Latents (Tier‑1 & Tier‑2):**
  - SBERT provides *clean, noise‑reduced embeddings* well suited to deterministic rails.  
  - Experiments (ngf‑alpha, Tier‑2) showed that SBERT latents combined with WDD rails
    yield >98% F1 on curated primitive sets.  
  - Strength: stability, low noise, ease of calibration.

- **LLM Latents (Tier‑3, planned):**
  - Richer, but noisy. Latents extracted from large decoder LLMs are high‑variance
    and context‑dependent.  
  - Hypothesis: with NGF rails (Warp–Detect–Denoise), even messy LLM latents can be
    stabilized, extending coverage beyond SBERT.  
  - Challenge: separating *signal wells* from diffuse activations without overfitting.

Mapper / Audit Separation
-------------------------
From Tier‑1 → Tier‑2, the **Mapper** (intent classification) and **Audit**
(safety/detection layer) were explicitly decoupled:

- **Mapper:** deterministic classifier mapping prompts → candidate primitives.  
- **Audit:** independent rails (PCA, prototypes, matched filters) that *verify*
  the candidate against nulls/foils and policy checks.  

Key insights from Tier‑2 audits:
- Tier‑1 audits were confidence‑threshold + policy checks.  
- Tier‑2 audits applied PCA projections, similarity margins, null calibration,
  and WDD rails for deterministic gates.  
- The auditor harness (see ``README_AUDITOR.md``) proved that separating mapping
  from auditing prevents tautology and improves abstain quality.  

This separation allows the auditor to abstain even when the mapper proposes a label,
increasing safety and reducing hallucinations 【180†TIER2AUDIT.md】【181†README_AUDITOR.md】.

Abstain Philosophy
------------------
Unlike mainstream LLMs which *always* produce an answer, NGF and Micro‑LMs treat
**ABSTAIN** as a principled, valid outcome:

- **When to abstain:**
  - Ambiguous mappings (overlapping wells, low margins).  
  - Off‑distribution inputs (junk prompts).  
  - Policy violations (e.g., LTV, HF, oracle freshness).  

- **Why abstain matters:**
  - Ensures **safety** in high‑stakes domains (finance, healthcare).  
  - Builds **trust**: users know silence/abstain means caution, not failure.  
  - Provides **auditability**: abstains carry explicit reasons (`low_conf`,
    `below_gates`, `policy_fail`, `ambiguous_or_mismatch`).  

- **Tier‑2 results:** auditor harness showed *zero hallucinations on OOD prompts*
  with high macro‑F1 on in‑domain tests 【181†README_AUDITOR.md】.

Research Direction
------------------
- Develop methods to warp/detect/denoise **LLM latents** while preserving abstain
  guarantees.  
- Formalize mapper/audit decoupling as a general pattern for micro‑LMs.  
- Expand abstain philosophy into a broader doctrine of **deterministic safety
  rails for AI reasoning**.

