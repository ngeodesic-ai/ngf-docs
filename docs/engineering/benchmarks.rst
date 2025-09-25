.. _engineering-testing-benchmarks:

Testing & Benchmarks
====================

Overview
--------
Testing and benchmarking are critical to ensure that Micro‑LMs behave
**deterministically**, abstain when appropriate, and meet domain safety policies.

Benchmarks are run through the ``micro-lm-bench`` CLI, which executes
domain‑specific pipelines (ARC, DeFi) on curated test sets and reports metrics.

Testing Strategy
----------------
The testing stack is layered across tiers:

- **Tier‑1 (Mapper focus):**  
  - Mapper trained on SBERT or wordmap embeddings.  
  - Benchmarks validate top‑1 accuracy across primitives.  
  - Determinism checked: identical prompts → identical labels.  
  - Policy verifiers (LTV, HF, oracle, schema checks) applied post‑mapping.

- **Tier‑2 (Auditor focus):**  
  - Introduces **WDD rails** on SBERT latents (PCA, matched filters, nulls/foils).  
  - Auditor harness verifies mapper predictions independently.  
  - Abstain quality improves: auditor can veto mapper misclassifications.  
  - No tautology: audit uses separate latent projections 【231†TIER2.md】.

- **Tier‑3 (Planned, LLM latents):**  
  - Auditor extended to messy LLM hidden states.  
  - Goal: preserve abstain determinism while broadening domain coverage.

Benchmark Files
---------------
Benchmarks are stored in JSONL format:

.. code-block:: json

    {"prompt": "deposit 10 ETH into aave", "label": "deposit_asset"}
    {"prompt": "swap 5 SOL into USDC on uniswap", "label": "swap_asset"}

CLI Example:

.. code-block:: bash

    micro-lm-bench defi \
      --file benches/defi_smoke.jsonl \
      --out .artifacts/defi_smoke_results.jsonl \
      --summary-out .artifacts/defi_smoke_summary.json \
      --gate-metric ok_acc --gate-min 0.66

Metrics
-------
Key metrics include:

- ``ok_acc``: accuracy on accepted prompts.  
- ``abstain_rate``: fraction of prompts abstained.  
- ``macro-F1``: balanced performance across primitives.  
- ``determinism``: % identical traces across repeated runs.  

Example Summary (smoke benchmark):  

.. code-block:: json

    {
      "total": 3,
      "ok": 2,
      "ok_acc": 0.6667,
      "abstain_rate": 0.3333
    }

SBERT Training (Stage-8)
------------------------
- SBERT embeddings trained/fine‑tuned on labeled primitives 【230†SBERT.md】.  
- Produces clean latent spaces for Tier‑1/Tier‑2.  
- Mapper is stored as ``.artifacts/defi_mapper.joblib``.  

Auditor Verification (Stage-9)
------------------------------
- Independent auditor built on PCA + WDD rails.  
- Uses matched filters + null calibration to detect foils.  
- Validates mapper predictions; can abstain if margins weak.  
- Produces **zero hallucinations** on out‑of‑domain prompts 【227†BENCHMARK.md】.

Integration into Stage-11
-------------------------
- Stage‑11 harness integrates mapper + auditor + policy verifiers.  
- All artifacts (mapper scores, auditor decisions, abstain reasons) logged.  
- Determinism validated under perturbation (synonyms, jitter).  
- Ensures reproducibility with explicit **ok/abstain** outputs.

