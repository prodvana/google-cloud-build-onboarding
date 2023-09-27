# Step 5: Create Your Application and Service

In this step, you will create a service that uses the Runtime Extension you defined previously. The goal of this step is for you to be able to trigger a Google Cloud Build from the Prodvana UI.

# Prereqs
- You must have completed all previous steps in this tutorial.
- You must install and authenticate [pvnctl](https://docs.prodvana.io/docs/pvnctl).

# Tutorial
1. Take the config files in `examples/`, modify them if you picked a different Runtime Extension name in the previous step. Fill in the correct values for `cloudbuild_project`, `cloudbuild_trigger`, and `substitutions` in `examples/applications/cloudbuild-app/services/cloudbuild-svc.pvn.yaml`.
2. Apply the configs with `pvnctl configs apply examples/...`.
3. Go to the Prodvana UI, find your service under your application, and kick off your first deployment.

Congratulations! You now have a Prodvana service that triggers your Google Cloud Build!