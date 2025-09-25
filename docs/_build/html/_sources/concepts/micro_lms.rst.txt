.. _concepts-micro-lms:

Micro-LMs Explained
===================

**Micro-LMs** are lightweight, domain-specialized AI *sidecars* that run alongside
large language models (LLMs) on **NGF rails** to turn natural language into
**deterministic, auditable actions** with built-in **safety and abstain** guarantees.

Why Micro-LMs?
--------------
- **Determinism:** Same inputs → same decisions (traceable, reproducible).
- **Domain focus:** Small, curated primitive sets (e.g., ARC ops, DeFi ops).
- **Safety-first:** Refuse (ABSTAIN) when uncertain instead of hallucinating.
- **Composability:** Plug into existing apps and LLMs without retraining.

Core Components
---------------
- **Mapper:** Interprets user intent and maps to domain primitives.
- **Rails:** The NGF pipeline (Warp → Detect → Denoise → Verify) that stabilizes decisions.
- **Verifiers:** Domain rules/policies (e.g., LTV/HF/oracle in DeFi).
- **Executor:** Applies the verified plan; or aborts if verifiers fail.

Example (DeFi)
--------------
A prompt like *"deposit 10 ETH into aave"* is mapped to a ``deposit_asset`` primitive.
Verifiers check collateralization, oracle age, and policy limits. If safe, the plan
is emitted; otherwise the system **ABSTAINS** with an explicit reason.
