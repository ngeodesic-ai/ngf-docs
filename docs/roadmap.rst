.. _roadmap:

Roadmap
=======

Overview
--------
The NGF + Micro‑LM ecosystem has completed **Tier‑1** (deterministic SBERT mappers)
and **Tier‑2** (SBERT + WDD auditors). The next phase extends into richer latents,
new domains, and open theoretical questions.

Tier-3: Sidecars with LLM Latents
---------------------------------
- **Goal:** swap SBERT embeddings for **LLM hidden states** as the mapper input.  
- **Challenge:** LLM latents are noisy, high‑variance, and context‑dependent.  
- **Approach:** apply NGF rails (Warp → Detect → Denoise) to stabilize latent
  manifolds, separating signal wells from diffuse activations.  
- **Outcome:** broaden coverage beyond curated SBERT primitives while retaining
  determinism and abstain guarantees.  

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
