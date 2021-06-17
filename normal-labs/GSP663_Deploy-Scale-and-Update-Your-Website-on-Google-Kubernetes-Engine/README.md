# GSP663 —— Deploy, Scale, and Update Your Website on Google Kubernetes Engine

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Architecture Diagram](#architecture-diagram)
- [Create GKE Cluster](#create-gke-cluster)
- [Create Docker Container with Cloud Build](#create-docker-container-with-cloud-build)
- [Deploy Container to GKE](#deploy-container-to-gke)
- [Expose GKE Deployment](#expose-gke-deployment)
- [Scale GKE deployment](#scale-gke-deployment)
- [Update with Zero Downtime](#update-with-zero-downtime)
- [Clean up](#clean-up)
- [References](#references)

</details>

## Overview

Running websites and applications is hard. Things go wrong when they shouldn't, servers crash, increase in demand causes more resources to be utilized, and making changes without downtime is complicated and stressful. Imagine if there was a tool that could help you do all this and even allow you to automate it. With Kubernetes, all of this is not only possible, it's easy!

In this lab you will assume the role of a developer at a fictional company, Fancy Store, running an ecommerce website. Due to problems with scaling and outages, you are tasked with deploying your application onto the Google Kubernetes Engine (GKE).

## Architecture Diagram

<div align="center">
  <img src="https://i.imgur.com/DmyTiM9.png" alt="Architecture Diagram">
</div>

## Create GKE Cluster

```bash
# enable the Container Registry API
$ gcloud services enable container.googleapis.com

# create GKE cluster
$ gcloud container clusters create <CLUSTER_NAME> --num-nodes="<NODE_NUMBER>"

# check instances
$ gcloud compute instances list
```

## Create Docker Container with Cloud Build

```bash
# enable the Cloud Build API
$ gcloud services enable cloudbuild.googleapis.com

# build docker container
$ gcloud builds submit --tag "<IMAGE_NAME>" .
```

## Deploy Container to GKE

```bash
# deploy application to GKE
$ kubectl create deployment monolith --image="<IMAGE_NAME>"

# check the pods status
$ kubectl get all
```

- Kubernetes represents applications as [Pods](https://kubernetes.io/docs/concepts/workloads/pods/)
  - Pods are units that represent a container (or group of tightly-coupled containers).
  - Pods are the smallest deployable units in Kubernetes.
- The Deployment manages multiple copies of your application, called replicas, and schedules them to run on the individual nodes in your cluster.

## Expose GKE Deployment

By default, the containers we run on GKE are not accessible from the Internet because they do not have external IP addresses. We must explicitly expose the application to traffic from the Internet via a [Service](https://kubernetes.io/docs/concepts/services-networking/service/) resource.

```bash
# expost website to the internet
$ kubectl expose deployment <POD_NAME> \
    --type="LoadBalancer" \
    --port="<PORT>" \
    --target-port="<TARGET_PORT>"

# inspect the services
$ kubectl get service
```

## Scale GKE deployment

Set up the replicas to scale our application to multiple instances so it can handle all this traffic.

```bash
# scale deployment replicas
$ kubectl scale deployment <POD_NAME> \
    --replicas="<REPLICAS_NUMBER>"

# check the pods status
$ kubectl get all
```

## Update with Zero Downtime

```bash
# update the image for deployment to a ewn version
$ kubectl set image deployment/<POD_NAME> <POD>=<IMAGE>

# validate deployment
$ kubectl get pods
```

## Clean up

```bash
# delete the container images
gcloud container images delete <IMAGE> --quiet

# delete Google Cloud Build artifacts from Google Cloud Storage
$ gcloud builds list | awk 'NR > 1 {print $4}'  # print all sources
$ gcloud builds list | awk 'NR > 1 {print $4}' | while read line; do gsutil rm $line; done

# delete GKE services
$ kubectl delete service <POD_NAME>
$ kubectl delete deployment <POD_NAME>

# delete GKE cluster
$ gcloud container clusters delete <CLUSTER_NAME>
```

## References

- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [Container Registry Documentation](https://cloud.google.com/container-registry/docs)