# Step 4: Create a Runtime Extension

In this step, you will take the Kubernetes Job spec created from previous steps and use it to create a [Runtime Extension](https://docs.prodvana.io/docs/runtime-extensions). The goal of this step is to create the Runtime Extension and ensure your configs are valid.

# Prereqs
- You must have completed all previous steps in this tutorial.
- You must install and authenticate [pvnctl](https://docs.prodvana.io/docs/pvnctl).

# Tutorial
1. Create a `.pvn.yaml` config file next to the `job.yaml` you created from previous steps. The config file defines your runtime extension. See `examples/` for the content of the file.
2. Apply your config file using `pvnctl configs apply path/to/your/config.pvn.yaml`. Prodvana will validate that your Kubernetes job spec is valid and that the namespace you chose exist.