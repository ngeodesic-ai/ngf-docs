.. _framework-ngeodesic-package:

ngeodesic Python Package
========================

Overview
--------
The **ngeodesic** package is the reference implementation of the
**Noetic Geodesic Framework (NGF)**. It provides the building blocks
for Warp–Detect–Denoise rails, and is the foundation on which
**Micro‑LMs** operate.

Key Features
------------
- **Warp:** PCA projection, funnel fitting, radial profiles.  
- **Detect:** Matched filters with dual thresholds (absolute vs null;
  relative vs best channel).  
- **Denoise:** Hybrid EMA+median smoothing, phantom guards, jitter
  averaging.  
- **Sidecar Hooks:** Interfaces to plug NGF rails into existing models.  
- **Parser API:** Stock parsers and full Stage‑11 geodesic parsers.  

Installation
------------

.. code-block:: bash

    pip install ngeodesic==0.0.2a1

Optional extras:

.. code-block:: bash

    pip install "ngeodesic[ml]"   # PCA/whitening (scikit-learn)
    pip install "ngeodesic[viz]"  # plots (matplotlib, scipy)
    pip install "ngeodesic[dev]"  # dev tools (pytest, ruff, mypy)

Quickstart Example
------------------

.. code-block:: python

    import numpy as np
    from ngeodesic.core.parser import geodesic_parse_report
    from ngeodesic.core.denoise import TemporalDenoiser

    rng = np.random.default_rng(42)
    n, T = 3, 160
    traces = [rng.normal(0, 0.3, T) for i in range(n)]
    keep, order = geodesic_parse_report(traces, sigma=9, proto_width=64)

    den = TemporalDenoiser(method="hybrid", ema_alpha=0.15, hybrid_k=3)
    smoothed = den.smooth(np.array([0.1, 0.4, 0.8, 0.6, 0.7]))

    print("Detected:", keep, "Order:", order)
    print("Smoothed:", smoothed)

Status & Roadmap
----------------
- **Status:** pre‑release (APIs stabilizing; tests/docs ongoing).  
- **Roadmap:** finalize Stage‑11 parser, integrate domain examples,
  expand benchmarks. 【214†README.md】
