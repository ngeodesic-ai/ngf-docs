.. _getting-started-quickstart:

Quickstart
===========================================

Python Example
--------------

.. code-block:: python

    from micro_lm.core.runner import run_micro

    # Define a simple DeFi prompt
    prompt = "deposit 10 ETH into aave"

    # Policy includes mapper and confidence threshold
    policy = {
        "mapper": {
            "model_path": ".artifacts/defi_mapper.joblib",
            "confidence_threshold": 0.5
        }
    }

    # Run the micro-LM sidecar
    res = run_micro(
        domain="defi",
        prompt=prompt,
        context={},
        policy=policy,
        rails="stage11",
        T=180,
        backend="wordmap"
    )

    print(res)

This produces a structured, auditable plan with verification info.

CLI Example
-----------

You can also run DeFi micro-LM via the CLI:

.. code-block:: bash

    micro-defi --prompt "deposit 10 ETH into aave" \
      --rails stage11 \
      --policy '{"mapper":{"model_path":".artifacts/defi_mapper.joblib","confidence_threshold":0.5}}'
