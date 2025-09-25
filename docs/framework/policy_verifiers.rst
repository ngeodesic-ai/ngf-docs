.. _framework-policy-verifiers:

Policy & Verifiers
==================

Overview
--------
Beyond NGF rails, **policy checks and verifiers** are applied to ensure
safe execution in domain‑specific micro‑LMs. These verifiers enforce
rules and block unsafe actions.

DeFi Verifiers
--------------
- **Loan‑to‑Value (LTV):** block if collateral ratio exceeds threshold.  
- **Health Factor (HF):** block if health factor < floor.  
- **Oracle freshness:** block if price feed is stale.  
- **Slippage bounds:** block unsafe swap parameters.

ARC Verifiers
-------------
- **Schema compliance:** ensure trace follows allowed primitive order.  
- **Ambiguity reduction:** abstain if multiple primitives are equally plausible.  
- **Input/output sanity:** validate grids are transformed correctly.

Audit vs Mapper
---------------
- **Mapper:** proposes candidate primitive.  
- **Audit:** applies NGF rails (WDD) + verifiers to accept or abstain.  
- **Policy checks:** final gating layer (e.g., LTV, HF).  

Together, mapper + rails + verifiers produce **deterministic,
auditable, safe plans**. 【203†DEFI_INTERFACE.md】【204†ARC_INTERFACE.md】
