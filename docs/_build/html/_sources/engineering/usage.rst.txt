.. _engineering-usage:

Usage
=========

Overview
--------
The **micro-lm** repository provides command‑line interfaces for running
deterministic micro‑LM pipelines on different domains and for benchmarking.

Available commands:
- ``micro-defi`` — run DeFi Micro‑LM prompts.  
- ``micro-arc`` — run ARC Micro‑LM prompts.  
- ``micro-lm-bench`` — benchmark pipelines across domains.  

micro-defi
----------
The ``micro-defi`` CLI runs prompts through the **DeFi Micro‑LM**.

Example:

.. code-block:: bash

    micro-defi --prompt "deposit 10 ETH into aave" \
      --rails stage11 \
      --policy '{"mapper":{"model_path":".artifacts/defi_mapper.joblib","confidence_threshold":0.7}}' \
      --context '{"oracle":{"age_sec":5,"max_age_sec":30}}'

Key Options:
- ``--prompt``: user prompt to interpret.  
- ``--rails``: rails backend (default: stage11).  
- ``--policy``: JSON schema with verifier thresholds (LTV, HF, oracle).  
- ``--context``: domain context (e.g., oracle age).  
- ``--verbose``: show mapper scores, audit, and verifier details.  

Output: JSON with plan, label, verification status, and abstain reasons.  
【229†DEFI_INTERFACE.md】

micro-arc
---------
The ``micro-arc`` CLI runs prompts through the **ARC Micro‑LM**.

Example:

.. code-block:: bash

    micro-arc --prompt "rotate the grid 90 degrees" \
      --rails stage11 --verbose

Key Options:
- ``--prompt``: ARC-style natural language instruction.  
- ``--rails``: rails backend (stage11 recommended).  
- ``--verbose``: show mapper, auditor, and trace routing.  

Output: JSON with structured plan, audit results, and abstain markers.  
【228†ARC_INTERFACE.md】

micro-lm-bench
--------------
The ``micro-lm-bench`` CLI runs domain benchmarks and reports metrics.

Example:

.. code-block:: bash

    micro-lm-bench defi \
      --file benches/defi_smoke.jsonl \
      --out .artifacts/defi_smoke_results.jsonl \
      --summary-out .artifacts/defi_smoke_summary.json \
      --gate-metric ok_acc --gate-min 0.66

Options:
- ``--file``: benchmark file (JSONL format).  
- ``--out``: output results JSONL.  
- ``--summary-out``: aggregated metrics.  
- ``--gate-metric``: metric to enforce (e.g., ok_acc).  
- ``--gate-min``: minimum threshold for passing.  
- ``--runs``: number of benchmark runs.  

Reports include total runs, abstains, pass/fail counts, and accuracy.  
【227†BENCHMARK.md】

Summary
-------
The CLIs provide reproducible, auditable interfaces for running and testing
Micro‑LMs across domains. They are designed to showcase **determinism, abstains,
and policy enforcement** with minimal setup.
