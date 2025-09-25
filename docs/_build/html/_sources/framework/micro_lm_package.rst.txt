.. _domains:

Domains
=======

Overview
--------
Micro‑LMs are **domain‑specialized sidecars** that apply NGF rails to enforce
deterministic, auditable reasoning. We pilot them in two domains:

1. **ARC Micro‑LM** — reasoning stress test.  
2. **DeFi Micro‑LM** — applied financial primitives.  

These serve as complementary proofs: ARC highlights reasoning power, while DeFi
demonstrates real‑world applicability.

ARC Micro-LM (Reasoning Stress Test)
------------------------------------
The **ARC (Abstraction & Reasoning Corpus)** domain provides a rigorous aptitude
benchmark where conventional LLMs often fail. ARC requires compositional
generalization over small grid transformations such as rotations and flips.

- **Canonical primitives:** ``rotate``, ``flip_h``, ``flip_v`` 【204†ARC_INTERFACE.md】.  
- **Pipeline:** Prompts + grids → mapper (ARC joblib) → NGF rails (Warp–Detect–Denoise).  
- **Modes:**  
  - *Tier‑1:* mapper audit only (confidence thresholds).  
  - *Tier‑2:* WDD detector audit (mapper still authoritative).  
  - *Tier‑2 family:* WDD supplies the primitive order.  
- **Output:** Structured plan with audit tags; abstains if ambiguous or off‑manifold.  

ARC is used as a **stress test** to highlight NGF’s ability to produce
deterministic traces even in reasoning‑heavy tasks 【206†README.md】.

DeFi Micro-LM (Finance Primitives)
----------------------------------
The **DeFi domain** is a business‑style usecase: mapping prompts about
decentralized finance into safe, auditable primitives.

- **Canonical primitives:** ``deposit_asset``, ``swap_asset``, ``withdraw_asset``,
  ``borrow_asset``, ``repay_asset``, ``stake_asset``, ``unstake_asset``,
  ``claim_rewards`` 【203†DEFI_INTERFACE.md】.  
- **Pipeline:** Prompts → SBERT mapper → NGF rails (Stage‑11).  
- **Verifiers:** Policy‑driven checks: Loan‑to‑Value (LTV), Health Factor (HF),
  Oracle freshness. Unsafe operations → block or abstain.  
- **Modes:**  
  - *Tier‑1:* mapper + confidence threshold + policy verifiers.  
  - *Tier‑2:* WDD audit (detector or family).  

Benchmarks show >98% accuracy on 8 primitives with principled abstains
【205†SBERT.md】【206†README.md】.

Cross-Domain Potential
----------------------
NGF rails and the Micro‑LM architecture generalize beyond ARC and DeFi:

- **Healthcare:** map clinical notes → structured medical orders, with dosage
  verifiers and drug‑interaction checks.  
- **Manufacturing & Robotics:** map operator prompts → deterministic motion plans,
  with collision checks and torque limits.  
- **Supply Chain:** convert planning instructions → deterministic workflows, with
  capacity and customs verifiers.  
- **Energy & Grid:** map operator commands → safe dispatch actions, with load
  balancing verifiers.  
- **Legal & Contracts:** parse clauses → compliance checks, with regulatory
  verifiers and abstain when ambiguous.

This cross‑domain flexibility shows that Micro‑LMs are not tied to one vertical,
but provide a **general recipe for safe deterministic reasoning**.

