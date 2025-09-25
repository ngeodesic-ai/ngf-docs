.. _getting-started-quickstart:

Quickstart
===========================================

Installation
--------------

You can install the core framework and tooling with pip:

.. code-block:: bash

    # Install the NGF rails package
    pip install ngeodesic

    # Install the micro-LM tooling package
    pip install micro-lm

For development (recommended), install from source:

.. code-block:: bash

    git clone https://github.com/ngeodesic-ai/ngeodesic.git
    cd ngeodesic && pip install -e .

    git clone https://github.com/ngeodesic-ai/micro-lm.git
    cd micro-lm && pip install -e .



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
