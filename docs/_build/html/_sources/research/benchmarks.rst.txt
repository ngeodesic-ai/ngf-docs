.. _research-ngf-alpha-benchmarks:

Benchmarks
=====================

Stage-11 introduced the breakthrough:

- **Warp:** Embed latents into PCA(3) space, warp into a single dominant well.
- **Detect:** Use matched filters with null calibration to identify the true well.
- **Denoise:** Apply smoothing, phantom guards, and jitter averaging to suppress false wells.

(Part A) Latent-ARC Results (n=100)
-----------------------------------

+-------------------+-----------+-----------+--------+--------+---------+----------+
| Model             | Exact Acc | Precision | Recall | F1     | Halluc. | Omission |
+===================+===========+===========+========+========+=========+==========+
| Denoise (Stage 11)| **1.000** | 0.9977    | 0.9989 | 0.9983 | 0.0045  | 0.0023   |
+-------------------+-----------+-----------+--------+--------+---------+----------+
| Geodesic (pre)    | 0.640     | 0.8450    | 1.0000 | 0.8980 | 0.1550  | 0.0000   |
+-------------------+-----------+-----------+--------+--------+---------+----------+
| Stock baseline    | 0.490     | 0.8900    | 0.7767 | 0.7973 | 0.1100  | 0.2233   |
+-------------------+-----------+-----------+--------+--------+---------+----------+

**Note (Part A):** Stock baseline approximates what you’d see if you used simple thresholds
on LLM latents/logits without NGF’s Warp → Detect → Denoise.

(Part B) LMM-HellaSwag Results (n=1000)
---------------------------------------

+-------------------+--------+------------------+-------------+-----------------------+
| Model             | F1     | ECE (Calibration)| Brier Score | Overconfidence > 0.70 |
+===================+========+==================+=============+=======================+
| MaxWarp (Stage 11)| 0.35   | 0.080            | 0.743       | 1.2%                  |
+-------------------+--------+------------------+-------------+-----------------------+
| Stock baseline    | 0.324  | 0.122            | 0.750       | 0.7%                  |
+-------------------+--------+------------------+-------------+-----------------------+
| Change (Δ)        | +0.032 | -0.032           | -0.007      | +0.5%                 |
+-------------------+--------+------------------+-------------+-----------------------+

.. figure:: /_static/stage11_well_compare.png
   :alt: NGF Warped vs Flat Paths
   :align: center
   :scale: 25%

   Fig 1. PCA-2 visualization of “semantic wells” (pre vs post warp) on GPT-2 (tap 9).



Key Results → Micro-LMs
-----------------------
1. **WDD Works in Practice**  
   The staged experiments confirmed that WDD reliably improved reproducibility,
   separation, and robustness. This validated NGF as more than theory—it was
   a working framework.

2. **Deterministic Traces**  
   By Stage‑11, identical prompts produced **identical traces and outcomes**
   across runs, a property absent in baseline models.

3. **Principled Abstains**  
   Experiments showed that ambiguity could be detected geometrically—when wells
   overlapped or margins were thin, abstains were triggered instead of guesses.

4. **Blueprint for Sidecars**  
   The insights from ngf‑alpha directly inspired **Micro‑LMs**: lightweight,
   domain‑specific reasoning sidecars that use NGF rails to map intent to
   primitives under verifiers.

   - **ARC Micro‑LM** became the reasoning stress test.  
   - **DeFi Micro‑LM** became the production‑style demo with policy checks.

