# GSP659 —— Deploy Your Website on Cloud Run

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Architecture Diagram](#architecture-diagram)
- [Create Container with Cloud Build](#create-container-with-cloud-build)
- [Deploy Container to Cloud Run](#deploy-container-to-cloud-run)
- [Make Change and Update with Zero Downtime](#make-change-and-update-with-zero-downtime)
- [Cleanup](#cleanup)
- [References](#references)

</details>

## Overview

Running websites can be difficult with all of the overhead of creating and managing VMs, clusters, pods, services, etc. This is fine for larger, multi-tiered applications, but if you are just trying to get your website deployed and visible, it's a lot of overhead.

With [Cloud Run](https://cloud.google.com/run), Google Cloud's implementation of [Google's KNative framework](https://cloud.google.com/knative/), you can manage and deploy your website without any of the infrastructure overhead you experience with a VM or pure Kubernetes-based deployments. Not only is this a simpler approach from a management perspective, it also gives you the ability to "scale to zero" when there are no requests coming into your website.

Cloud Run brings "serverless" development to containers and can be run either on your own Google Kubernetes Engine (GKE) clusters or on a fully managed PaaS solution provided by Cloud Run. You will be running the latter scenario in this lab.

## Architecture Diagram

<div align="center">
  <img src="https://i.imgur.com/novJ8P4.png" alt="Architecture diagram">
</div>

Begin with a Docker image created via Cloud Build, which gets triggered from Cloud Shell, then deploy the image out to Cloud Run from a command in Cloud Shell.

## Create Container with Cloud Build

```bash
# enable the Cloud Build API
$ gcloud services enable cloudbuild.googleapis.com

# build docker container
$ gcloud builds submit --tag="gcr.io/<PROJECT_ID>/<TAG>:<VERSION>" .
```

- Cloud Build can be used to build the docker container and upload image in Container Registry.
- Cloud Build will compress the files and move them to a Cloud Storage bucket.
- Image will be pushed to Container Registry if we specified the `--tag` flag with the host.

## Deploy Container to Cloud Run

There are two approaches for deploying to Cloud Run:

- **Managed Cloud Run**: The Platform as a Service model where all container lifecycle is managed by the Cloud Run product itself.
- **Cloud Run on GKE**: Cloud Run with an additional layer of control which allows you to bring your own clusters & pods from GKE. You can read more about it here.

Let's use the first approach to deploy image to Cloud Run.

```bash
# enable Cloud Run API
$ gcloud services enable run.googleapis.com

# deploy application
$ gcloud run deploy --image=<IMAGE_NAME> --platform="managed"

# verify the deployment was created
$ gcloud run services list
```

- Cloud Run application will have a concurrency value of 80 by default. It means that each container instance will serve up to 80 requests at a time.
- The Functions-as-a-Service model, where one instance handles only one request at a time.

## Make Change and Update with Zero Downtime

Once the code is updated, we can rebuild the docker container and publish it to Container Registry by adding version label with previous command.

```bash
# rebuilt docker container and update version
$ gcloud builds submit --tag="gcr.io/<PROJECT_ID>/<TAG>:<UPDATE_VERSION>" .

# deploy application
$ gcloud run deploy --image=<IMAGE_NAME> --platform="managed"
```

Cloud Run treats each deployment as a new Revision which will first be brought online, then have traffic redirected to it. By default the latest revision will be assigned 100% of the inbound traffic for a service. It is possible to use "Routes" to allocate different percentages of traffic to different revisions within a service.

## Cleanup

Run the following to delete Container Registry images:

```bash
# delete container image
$ gcloud container images delete <IMAGE> --quiet

Run the following to delete Cloud Build artifacts from Cloud Storage:


# delete Cloud Build artifacts from Cloud Storage
$ gcloud builds list | awk 'NR > 1 {print $4}'  # print all sources
$ gcloud builds list | awk 'NR > 1 {print $4}' | while read line; do gsutil rm $line; done

# delete Cloud Run service
$ gcloud beta run services delete monolith --platform="managed"
```

## References

- [Cloud Build Documentation](https://cloud.google.com/build/docs)
- [Cloud Run Documentation](https://cloud.google.com/run/docs)