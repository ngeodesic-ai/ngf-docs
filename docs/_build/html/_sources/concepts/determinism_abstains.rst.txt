.. _concepts-determinism-abstains:

Determinism & Abstains
======================

Determinism
-----------
Micro-LMs target **deterministic decisioning**: identical inputs produce **identical
traces and outcomes**. This supports audit, debugging, and compliance.

- Same prompt, context, rails, and policy → same plan and verifier outputs.
- Determinism is enforced by WDD rails (warp/detect/denoise) plus strict policy checks.

Abstains
--------
When uncertainty or policy violations occur, Micro-LMs **ABSTAIN** rather than
guess. Abstains are **first-class outcomes** with explicit reasons (e.g.,
``abstain_non_exec``, ``ambiguous_or_mismatch``, ``policy_violation``).

Why it matters
--------------
- **Safety:** prevents harmful or costly actions (e.g., incorrect DeFi operations).
- **Trust:** stakeholders can rely on predictable, explainable behavior.
- **Compliance:** auditable traces support regulatory and internal reviews.

Best Practices
--------------
- Set a **confidence threshold** for the mapper.
- Treat abstains as **signals** to refine prompts, policy, or training data.
- Log and review abstain reasons to improve domain coverage safely.
