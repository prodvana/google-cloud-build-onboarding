# Step 3: Link Your Cluster to Prodvana

In this step, you will link your cluster to Prodvana and start a simple nginx service. The goal of this step is to ensure that you have a functioning Kubernetes cluster that can be used with Prodvana.

# Prereqs
- You must have completed all previous steps in this tutorial.
- You must have a Prodvana account (talk to us if you don't have one).

# Tutorial
Follow the [online tutorial](https://docs.prodvana.io/docs/deploying-nginx-on-prodvana) from our docs using the cluster you created from the previous steps. Note that you will not need your Job spec from the previous step in this step.
- Note: if you are using GKE Autopilot, when you first link your cluster, it can take several minutes for Prodvana Agent to start up and connect to Prodvana.