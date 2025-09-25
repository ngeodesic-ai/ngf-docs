Interface - DeFi
====================

This is the single, living reference for how to drive **micro-lm** via the **quickstart** entry point (CLI + Python).  
It unifies Tier-1 and Tier-2 semantics across **DeFi** and **ARC** and explains how flags interact.

0) TL;DR presets
----------------

**Tier-1 (mapper audit only, no WDD)**

.. code-block:: bash

   python3 -m micro_lm.cli.defi_quickstart "swap 2 ETH for USDC" \
     --rails stage11 \
     --policy '{"mapper":{"model_path":".artifacts/defi_mapper.joblib","confidence_threshold":0.70}}' \
     --verbose

**Tier-2 (WDD detector audit; mapper decides action)**

.. code-block:: bash

   python3 -m micro_lm.cli.defi_quickstart "deposit 10 ETH into aave" \
     --rails stage11 \
     --policy '{"audit":{"backend":"wdd"},"mapper":{"confidence_threshold":-1.0}}' \
     --verbose

**Tier-2 (WDD family; WDD supplies plan)**

.. code-block:: bash

   python3 -m micro_lm.cli.defi_quickstart "swap 2 ETH for USDC" \
     --rails stage11 \
     --policy '{"audit":{"backend":"wdd","mode":"family","K":12,"template_width":64,"z_abs":0.55,"keep_frac":0.70}}' \
     --verbose

**Edge block (example: DeFi LTV/HF/oracle)**

.. code-block:: bash

   python3 -m micro_lm.cli.defi_quickstart "withdraw 5 ETH" \
     --rails stage11 \
     --policy '{"ltv_max":0.60,"mapper":{"confidence_threshold":-1.0}}' \
     --context '{"oracle":{"age_sec":5,"max_age_sec":30},"risk":{"hf":1.15}}' \
     --verbose

1) The single entry point
-------------------------

- **CLI**::

    python3 -m micro_lm.cli.<domain>_quickstart "<prompt>" [--rails <stage>] [--policy JSON] [--context JSON] [--verbose]

- **Python**::

    from micro_lm.cli.<domain>_quickstart import quickstart

    quickstart(prompt, policy=None, context=None, rails="stage11", T=180)

**Uniform output contract** (both domains):

.. code-block:: json

   {
     "prompt": str,
     "domain": "defi" | "arc",
     "rails": "stage11",
     "T": int,
     "top1": str|null,
     "sequence": [str],
     "plan": {"sequence": [str]},
     "verify": {"ok": bool, "reason": str, "tags": [str]},
     "flags": { ... },
     "aux": { "stage11": { "wdd": {...} }, ... },
     "wdd_summary": { "decision": "PASS"|"ABSTAIN"|null, "keep": [...], "sigma": int|null, "proto_w": int|null, "which_prior": str|null, "note": str|null },
     "det_hash": str,
     "abstained": bool
   }

Key invariants:

- ``plan.sequence`` emits **canonical primitives** (e.g., ``swap_asset``, ``deposit_asset``).
- If ``verify.ok == false`` (or reason contains a blocking keyword), **plan is cleared**: ``plan.sequence = []``.

2) Policy schema (flags)
------------------------

**2.1 ``policy.mapper`` (Tier-1 audit; “action source” in all tiers)**

+-----------------------+--------+---------+---------------------------------------------------------------+
| Key                   | Type   | Default | Meaning                                                       |
+=======================+========+=========+===============================================================+
| ``model_path``        | str    | null    | Path to trained mapper (joblib).                              |
+-----------------------+--------+---------+---------------------------------------------------------------+
| ``confidence_threshold`` | float | 0.70 | Tier-1 audit gate; if score < τ, mapper abstains. For Tier-2, |
|                       |        |         | set to ``-1.0`` or use ``skip_gate`` to disable.              |
+-----------------------+--------+---------+---------------------------------------------------------------+
| ``skip_gate``         | bool   | false   | If ``true``, ignores ``confidence_threshold`` entirely.        |
+-----------------------+--------+---------+---------------------------------------------------------------+

Notes:

- The mapper is the **authoritative action chooser**.
- For **Tier-2**, disable the gate (``confidence_threshold:-1.0`` or ``skip_gate:true``) so WDD is the audit.

**2.2 ``policy.audit`` (Tier-2 audit)**

+------------------+--------+-------------+------------------------------------------------------------+
| Key              | Type   | Default     | Meaning                                                    |
+==================+========+=============+============================================================+
| ``backend``      | enum   | null        | Set to ``"wdd"`` to enable WDD.                            |
+------------------+--------+-------------+------------------------------------------------------------+
| ``mode``         | enum   | "detector"  | ``"detector"`` (audit only) or ``"family"`` (WDD orders). |
+------------------+--------+-------------+------------------------------------------------------------+
| ``gate``         | bool   | false       | If ``true``, overwrite ``verify.ok



