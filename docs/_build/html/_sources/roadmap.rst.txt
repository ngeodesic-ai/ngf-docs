.. _roadmap:

Roadmap
=======

Overview
--------
The NGF + Micro‑LM ecosystem has completed **Tier‑1** (deterministic SBERT mappers)
and **Tier‑2** (SBERT + WDD auditors). The next phase extends into richer latents,
new domains, and open theoretical questions.


Tier-0: Baseline Deterministic Rails (✔ Secured)
------------------------------------------------
- **Stock matched filter + parser** pipeline.  
- Supports core DeFi primitives with deterministic abstain paths.  
- Sandbox verified and benchmarked with stable execution.

**Status:** ✅ Complete — foundation secured.

---

Tier-1: Micro-LM on SBERT Latents (✔ Secured)
---------------------------------------------
- Replace hashmap lookups with a **trained micro-LM encoder**.  
- Train against **2–5k SBERT latent prompts**.  
- Audit results to return ABSTAIN / PASS with auditable trace.  
- Benchmark with full Stage-11 runner on DeFi suites (**1% hallucination / 0.98 F1 Score** across 8 primitives).  

**Status:** ✅ Complete — MVP secured.

---

Tier-2: Incorporate WDD with SBERT Latents (✔ Secured)
------------------------------------------------------
The current release implements **Warp → Detect → Denoise (WDD)** on SBERT embeddings.

**Core Features**
- Deterministic mapper + verifier with abstain-first behavior.  
- Handles both DeFi prompts (financial primitives) and ARC prompts (cognitive/aptitude tasks).  
- Auditable traces: every PASS/ABSTAIN decision includes reasons + confidence.  
- Stress-tested on SBERT latents: validated signal separation + denoising.  

**Status:** ✅ Complete — WDD secured.  
**Purpose:** **Community Edition**, deterministic & auditable safety (but scoped), SBERT + WDD — Apache 2.0.

---

Tier-3: LLM Latents + WDD (🔮 Future / Enterprise)
--------------------------------------------------
The end-goal is to extend WDD beyond SBERT into large language model hidden states.

**Planned Features**
- Swap SBERT latents for LLM internal latents.  
- Apply WDD rails to noisy LLM embeddings → restore determinism.  
- Package as a sidecar system: LLM provides fluency, micro-LM provides deterministic safety.  
- Designed for enterprise use: auditability, compliance, SLAs.  

**Status:** 🔮 Planning stage — not required for MVP, proprietary development path.  
**Purpose:** **Enterprise Edition**: gold standard, LLM Latents + WDD — proprietary.


Future Domains
--------------
Micro‑LMs can extend beyond ARC and DeFi into other high‑stakes or structured domains:

- **Healthcare:** clinical notes → orders with dosage verifiers.  
- **Manufacturing/Robotics:** operator prompts → deterministic motion plans with
  collision/torque checks.  
- **Supply Chain:** planning instructions → workflows with capacity/customs checks.  
- **Energy/Grid:** operator dispatch → safe load balancing actions.  
- **Legal/Contracts:** clause parsing → compliance checks, abstains on ambiguity.  

These domains all benefit from NGF’s **determinism, abstains, and auditability**.

Open Research Questions
-----------------------
1. **Latent Generalization:** how best to warp/detect/denoise noisy LLM latents?  
2. **Audit/Mapper Dynamics:** can we formalize auditor vs mapper as a general
   pattern for sidecar AI systems?  
3. **Abstain Philosophy:** what are the limits of abstain‑first reasoning, and
   how can abstains be integrated into human‑AI workflows?  
4. **Scalability:** how do NGF rails scale as domain complexity grows (more
   primitives, larger context windows)?  
5. **Cross‑Domain Bridges:** can one Micro‑LM share priors or rails with another,
   or must each be trained/audited independently?  

Summary
-------
The roadmap is ambitious but clear: **extend NGF rails to LLM latents, expand
Micro‑LM applications to critical domains, and refine abstain‑centric reasoning
into a universal safety doctrine for AI.**
