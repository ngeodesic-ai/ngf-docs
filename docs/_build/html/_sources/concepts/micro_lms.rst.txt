.. _concepts-micro-lms:

Micro-LMs
===================

Micro-LMs are lightweight, domain-specialized AIs that run on NGF rails, turning natural language into deterministic, auditable actions with built-in safety and abstain guarantees. We are piloting this idea first on ARC (Abstraction & Reasoning Corpus) testing to highlight its reasoning power, then for DeFi (Decentralized Finance) to highlight it applicability (one of many verticals) — both built on top of the ngeodesic Python package.

**Attributes**

- **Determinism:** Same inputs → same decisions (traceable, reproducible).
- **Domain focus:** Small, curated primitive sets (e.g., ARC ops, DeFi ops).
- **Safety-first:** Refuse (ABSTAIN) when uncertain instead of hallucinating.
- **Composability:** Plug into existing apps and LLMs without retraining.


LLMs vs. micro-LMs 
-------------------

- **LLM = generalist**: broad knowledge, flexible language, but *stochastic and unsafe* for mission-critical execution.  
- **micro-LM = specialist**: slim, deterministic, auditable, and **more accurate where it matters** (DeFi/Finance, Manufacturing & Robotics, Industrial Robotics, Supply Chain & Logistics, Energy & Grid Management, etc).

+-------------------------+-------------------------------------------------------------+-------------------------------------------------------------------+
| Dimension               | LLMs (ChatGPT, Claude, Meta, Perplexity, etc.)              | **micro-LMs (ARC, DeFi)**                                         |
+=========================+=============================================================+===================================================================+
| **Domain accuracy**     | Broad coverage, but DeFi primitives are not a training      | Mapper trained on 1k–5k usecase prompts (e.g., DeFi, ARC).        |
|                         | focus. Accuracy drifts under phrasing changes.              | Benchmarked accuracy > 98% on 8 DeFi primitives; abstains         |
|                         |                                                             | correctly when uncertain.                                         |
+-------------------------+-------------------------------------------------------------+-------------------------------------------------------------------+
| **Determinism**         | Outputs vary run-to-run (sampling drift). Even              | Stage-11 NGF rails (Warp → Detect → Denoise) yield reproducible   |
|                         | ``temperature=0`` doesn’t guarantee identical results.      | traces. Perturbation tests confirm stable decisions.              |
+-------------------------+-------------------------------------------------------------+-------------------------------------------------------------------+
| **Safety / Policy       | Can be prompted with “stay under LTV 0.75,” but no hard     | Built-in verifiers: Loan-to-Value (LTV), Health Factor (HF),      |
| enforcement**           | guarantees — may still propose unsafe actions.              | Oracle freshness. Unsafe paths always block or abstain.           |
+-------------------------+-------------------------------------------------------------+-------------------------------------------------------------------+
| **Abstain behavior**    | Rarely abstains — tends to “make something up” even when    | Explicit abstain mode: non-exec prompts (balance checks, nonsense)| 
|                         | uncertain.                                                  | → abstain with clear reason (``abstain_non_exec``).               |
+-------------------------+-------------------------------------------------------------+-------------------------------------------------------------------+
| **Auditability**        | Opaque; no structured rationale.                            | Every run produces machine-readable artifacts: mapper score,      |
|                         |                                                             | abstain reason, verifier tags, plan trace. Auditable for          |
|                         |                                                             | compliance.                                                       |
+-------------------------+-------------------------------------------------------------+-------------------------------------------------------------------+
| **Efficiency / Cost**   | 10s–100s of billions of params; inference is slow/expensive.| SBERT (~22M params) + lightweight classifier. Fast, cheap,        |
|                         |                                                             | deployable in CI.                                                 |
+-------------------------+-------------------------------------------------------------+-------------------------------------------------------------------+
| **Regulatory /          | Hard to certify (stochastic, unexplainable).                | Deterministic + auditable by design. Built for domains where      |
| Compliance fit**        |                                                             | regulators demand safety.                                         |
+-------------------------+-------------------------------------------------------------+-------------------------------------------------------------------+



Core Components
---------------
- **Mapper:** Interprets user intent and maps to domain primitives.
- **Rails:** The NGF pipeline (Warp → Detect → Denoise → Verify) that stabilizes decisions.
- **Verifiers:** Domain rules/policies (e.g., LTV/HF/oracle in DeFi).
- **Executor:** Applies the verified plan; or aborts if verifiers fail.

Examples 
--------------

**DeFi**
A prompt like *"deposit 10 ETH into aave"* is mapped to a ``deposit_asset`` primitive.
Verifiers check collateralization, oracle age, and policy limits. If safe, the plan
is emitted; otherwise the system **ABSTAINS** with an explicit reason.
