# Step 2: Create a Kubernetes Job Spec for Triggering Cloud Build

In this step, you will create a Kubernetes [Job](https://kubernetes.io/docs/concepts/workloads/controllers/job/) spec to trigger and monitor a Cloud Build. The goal of this step is to validate that you have a functioning Kubernetes cluster with the correct permissions to trigger Cloud Build.

## Prereqs
- You must complete all previous steps in the tutorial.
- You must have a Google Cloud Build trigger already created.

## Tutorial

1. Create a Kubernetes Job spec. We have provided a starting point under `examples/job.yaml`. Take this yaml, replace all instances of `{{.Params.*}}` with their appropriate values.
    a. `{{.Params.cloudbuild_project}}` - your GCP project that contains the Cloud Build trigger
    b. `{{.Params.substitutions}}` - your Cloud Build trigger substitutions in the format NAME=VALUE
    c. `{{.Params.version}}` - a tag that exists on the repo you have linked to Cloud Build. This will be used to start off a new Cloud Build.
2. Create an instance of the job by via `kubectl`. The namespace should be what you picked out in step 1.
```
kubectl -n cloudbuild-trigger create -f job.yaml
```
3. Check if your job succeeds. You can use the GCP console or some of the following handy commands to debug the job.
```
kubectl -n cloudbuild-trigger get jobs
kubectl -n cloudbuild-trigger logs [-f] jobs/{job-name}
```
4. If your job succeeds, you are done. If it does not, you may need to fix up permissions.
5. If you modify `job.yaml` beyond substituting in the parameters, create a new `job.yaml` with `{{.Params.*}}` untouched and your modifications. `{{.Params.*}}` will be substituted in by Prodvana at a later step.