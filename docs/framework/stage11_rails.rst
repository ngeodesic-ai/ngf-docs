.. _framework-stage11-rails:

Stage-11 Rails in Detail
========================

Overview
--------
**Stage‑11 rails** are the canonical NGF pipeline: Warp → Detect → Denoise.
They stabilize latent trajectories to yield reproducible, deterministic
reasoning traces.

Components
----------
1. **Warp**  
   - PCA(3) projection of latents.  
   - Radial funnel profile fitting.  
   - Curvature/depth metrics for semantic wells.

2. **Detect**  
   - Residual channels per primitive.  
   - Unimodal matched filter.  
   - Dual thresholds: relative vs best channel, absolute vs null (permuted).

3. **Denoise**  
   - Hybrid EMA+median smoothing.  
   - Phantom guard probes.  
   - Jitter averaging to enforce reproducibility.

Quickstart
----------
.. code-block:: bash

    ngeodesic-stage11-demo
    # expect: truth [1, 2] / pred [1, 2] / keep [False, True, True]

Design Goals
------------
- Suppress hallucinations and phantom wells.  
- Enforce deterministic traces across repeated runs.  
- Support sidecar integration with micro‑LMs. 【214†README.md】
