# Step 1: Create the Control Kubernetes Cluster With Permission to Trigger Cloud Build.

The control Kubernetes cluster will be used to run jobs to manage Cloud Build. The goal of this step is to prepare your environment to connect to Prodvana.

## Prereqs
- You must have access to the GCP console with the necessary permissions to create a Kubernetes cluster and a service account.
- You must have `gcloud` installed and authenticated.

## Tutorial

1. Create a Kubernetes cluster. This is best done via the GCP console, by going to "Kubernetes Engine", "Create", then leaving default options.
2. (Skip if you used a public network, the default option, earlier): If you choose to make your cluster have a private network, you must also configure a NAT and attach it to the default network. This is needed so that your cluster can communicate with Prodvana.
    a. Go to "Cloud NAT", "CREATE CLOUD NAT GATEWAY", fill in the form (create a router if needed). Make sure to choose the same network as the one your Kubernetes cluster uses.
3. Create a service account for triggering Cloud Build. This is best done via the GCP console, by going to "Service Accounts", "CREATE A SERVICE ACCOUNT". You can skip adding roles and principals.
4. Give your service account the necessary permissions. If your Cloud Build trigger is in a different GCP project, make sure to use the correct GCP project when granting the permissions.
    a. roles/cloudbuild.builds.editor - allows starting Cloud Builds
    b. roles/logging.viewer - if your build logs are in Logging, OR
    c. roles/viewer - if your build logs are in the default Google-created Cloud Storage bucket
    d. You can also use the following `gcloud` commands to grant permissions:
```
gcloud projects add-iam-policy-binding {project-with-cloud-build} --member=serviceAccount:{service-account-name}@{project-with-control-cluster}.iam.gserviceaccount.com --role=roles/cloudbuild.builds.editor
gcloud projects add-iam-policy-binding {project-with-cloud-build} --member=serviceAccount:{service-account-name}@{project-with-control-cluster}.iam.gserviceaccount.com --role=roles/logging.viewer
gcloud projects add-iam-policy-binding {project-with-cloud-build} --member=serviceAccount:{service-account-name}@{project-with-control-cluster}.iam.gserviceaccount.com --role=roles/viewer
```
5. Download the JSON key for your service account. This is best done via the GCP console, by going to "Service Accounts", your service account, "Keys", "Add Key", "Create a New Key", "JSON".
6. [Install kubectl](https://kubernetes.io/docs/tasks/tools/).
7. Authenticate kubectl to your newly created cluster. This is best done via the GCP console, by going to "Kubernetes Engine", your cluster, "CONNECT" and pasting the `gcloud` command. Note that your cluster must already be fully up and healthy.
8. Create a namespace that Prodvana will use to execute jobs in. The name can be whatever you want. This tutorial uses `cloudbuild-trigger`.
```
kubectl create namespacee cloudbuild-trigger
```
9. Upload your service account key to Kubernetes as a Secret. The secret name can be whatever you want. This tutorial uses `cloudbuild-sa-key`.
```
kubectl create -n cloudbuild-trigger secret generic cloudbuild-sa-key --from-file=key.json={downloaded}.json
```