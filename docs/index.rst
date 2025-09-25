.. _getting-started-introduction:

Introduction
==============================

Ngeodesic provides safety guardrails for AI with enhanced performance. Our Micro-LM sidecars act as a **Layer 2 for AI**: improving efficiency and reliability, enforcing determinism, auditability, and compliance — all while letting large language models remain fluent and flexible. For GitHub repos, you can visit:

* `NGF Research <https://github.com/ngeodesic-ai/ngf-alpha>`_
* `micro-LM <https://github.com/ngeodesic-ai/micro-lm>`_

Warp->Detect->Denoise (WDD)
-------------------------------
Warp → Detect → Denoise (WDD) is a patented pipeline for making noisy latent spaces deterministic and auditable. It first warps embeddings into a stable geometry, then detects true signals with calibrated filters, and finally denoises phantom attractors. The result: reproducible PASS/ABSTAIN decisions with clear traces — turning stochastic LLM outputs into predictable, safe, enterprise-grade behavior.

.. image:: /_static/ngf_warped_geodesic_contour.gif
   :alt: NGF Warped vs Flat Paths
   :align: center
   :scale: 70%

Micro-LMs
-------------------------------
Micro-LMs are lightweight, domain-specific companions to LLMs that provide determinism, safety, and auditability. They focus on a narrow set of primitives (e.g., DeFi actions, ARC puzzles), mapping prompts into PASS or ABSTAIN with verifiers and traces. The LLM handles fluency, while the micro-LM enforces guardrails and compliance — the best of both worlds.


Micro-LM Sidecar 
-------------------------------

A **Micro-LM Sidecar** can be thought of as a **Layer 2 for AI**: it doesn’t replace the large language model, but it sits alongside it to improve performance, add safety guardrails, determinism, and auditability. In AI, the LLM is like Layer 1: broad, powerful, but stochastic and sometimes unsafe. A Micro-LM Sidecar is like Layer 2: lightweight, domain-specific, enforcing determinism and safety guardrails, but still “anchored” to the LLM’s fluency and reasoning power.

**Request Cycle**

.. code-block:: bash

    User → LLM → /decide {prompt, context, policy}
                     ↓
               SBERT → PCA → map → θ → guards
                     ↓
       ← {approve|reject|abstain, reason, plan, trace_id}

- LLM explains/asks confirm
- User confirms
- LLM → /execute {trace_id, plan}
- Sidecar re-checks guards → tools (if OK) → finalize trace


**Workstream Breakdown**

.. note::
   Status icons legend — ✅ Built • 🟡 Partial • 🔴 Planning

+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Workstream              | What it covers                                | Component   | Status  | % Effort | % Done  |
+=========================+===============================================+=============+=========+==========+=========+
| WDD R&D                 | Research, math, validation of Warp → Detect → | WDD         | ✅      | 30%      | 30%     |
|                         | Denoise (ngf-alpha, DeFi/ARC, proofs).        |             |         |          |         |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Core pipeline (R&D)     | SBERT → PCA prototyping, thresholds, datasets | Micro-LM    | ✅      | 15%      | 13%     |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Core pipeline           | Engineering impl. of SBERT → PCA/θ,           | Micro-LM    | ✅      | 20%      | 17%     |
| (Engineering)           | integration with WDD-lite.                    |             |         |          |         |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Domain guards           | HF / LTV / oracle freshness verifiers.        | Micro-LM    | ✅      | 10%      | 8%      |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Plans & policies        | Primitive specs, per-class thresholds,        | Micro-LM    | ✅      | 5%       | 4%      |
|                         | policy defaults.                              |             |         |          |         |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Quickstart harness      | In-process run + JSON outputs.                | Micro-LM    | ✅      | 5%       | 4%      |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Tests & canaries        | Smoke cases, threshold checks.                | Micro-LM    | 🟡      | 5%       | 3%      |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| API layer               | ``/decide``, ``/execute``, schemas.           | Sidecar     | 🔴      | 4%       | 0%      |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Orchestrator glue       | Routing, retries, caches.                     | Sidecar     | 🔴      | 2%       | 0%      |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Observability           | Logs, metrics, ``/healthz`` & ``/version``.   | Sidecar     | 🔴      | 2%       | 0%      |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Audit trail             | Structured traces, IDs.                       | Sidecar     | 🟡      | 1%       | 0.3%    |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+
| Ops safety              | Warmup, kill-switch, double-gate at execute.  | Sidecar     | 🟡      | 1%       | 0.2%    |
+-------------------------+-----------------------------------------------+-------------+---------+----------+---------+

**Total % Done ≈ 85% (±5%).**



Our first pilots are:

- **ARC Micro-LM** → reasoning stress test (Abstraction & Reasoning Corpus).
- **DeFi Micro-LM** → finance primitives with verifiers for safety and risk control.

If you are a researcher, developer, or just curious about deterministic AI reasoning,
this guide will help you get started quickly.


.. toctree::
    :maxdepth: 1
    :hidden:
    :caption: Getting Started

    Home <self>      
    quickstart
    roadmap
    licencing

.. toctree::
    :maxdepth: 3
    :hidden:
    :caption: Concepts

    concepts/micro_lms
    concepts/ai_reasoning

.. toctree::
    :maxdepth: 3
    :hidden:
    :caption: Research

    research/ngf
    research/benchmarks
    research/publications_patents

.. toctree::
    :maxdepth: 3
    :hidden:
    :caption: Engineering

    engineering/interface_arc
    engineering/interface_defi
    engineering/repository_structure


