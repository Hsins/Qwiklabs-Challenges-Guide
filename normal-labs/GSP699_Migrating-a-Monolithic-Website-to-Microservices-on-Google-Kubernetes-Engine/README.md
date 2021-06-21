# GSP699 —— Migrating a Monolithic Website to Microservices on Google Kubernetes Engine

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Introduction](#introduction)
- [Architecture Diagram of Our Microservices](#architecture-diagram-of-our-microservices)
- [Create GKE Cluster](#create-gke-cluster)
- [Deploy Monolith Application](#deploy-monolith-application)
- [Migrate Monolithic Application to Microservice](#migrate-monolithic-application-to-microservice)
- [References](#references)

</details>

## Introduction

Why migrate from a monolithic application to a microservices architecture? Breaking down an application into microservices has the following advantages, most of these stem from the fact that microservices are loosely coupled:

- The microservices can be independently tested and deployed. The smaller the unit of deployment, the easier the deployment.
- They can be implemented in different languages and frameworks. For each microservice, you're free to choose the best technology for its particular use case.
- They can be managed by different teams. The boundary between microservices makes it easier to dedicate a team to one or several microservices.
- By moving to microservices, you loosen the dependencies between the teams. Each team has to care only about the APIs of the microservices they are dependent on. The team doesn't need to think about how those microservices are implemented, about their release cycles, and so on.
- You can more easily design for failure. By having clear boundaries between services, it's easier to determine what to do if a service is down.

Some of the disadvantages when compared to monoliths are:

- Because a microservice-based app is a network of different services that often interact in ways that are not obvious, the overall complexity of the system tends to grow.
- Unlike the internals of a monolith, microservices communicate over a network. In some circumstances, this can be seen as a security concern. [Istio](https://cloud.google.com/learn/what-is-istio) solves this problem by automatically encrypting the traffic between microservices.
- It can be hard to achieve the same level of performance as with a monolithic approach because of latencies between services.
- The behavior of your system isn't caused by a single service, but by many of them and by their interactions. Because of this, understanding how your system behaves in production (its observability) is harder. Istio is a solution to this problem as well.

## Architecture Diagram of Our Microservices

Start by breaking the monolith into three microservices, one at a time. The microservices include, Orders, Products, and Frontend. Build a Docker image for each microservice using Cloud Build, then deploy and expose the microservices on Google Kubernetes Engine (GKE) with a Kubernetes service type LoadBalancer. You will do this for each service while simultaneously refactoring them out of the monolith. During the process you will have both the monolith and the microservices running until the very end when you are able to delete the monolith.


<div align="center">
  <img src="https://i.imgur.com/2z3bO5x.png" alt="Architecture Diagram">
</div>

## Create GKE Cluster

```bash
# enable the Containers API
$ gcloud services enable container.googleapis.com

# create GKE cluster
$ gcloud container clusters create <CLUSTER_NAME> --num-nodes="<NODES_NUMBER>"

# check cluster instances
$ gcloud compute instances list
```

## Deploy Monolith Application

```bash
# find the external IP address
$ kubectl get service <SERVICE_NAME>
```

## Migrate Monolithic Application to Microservice

```bash
# create Docker containers using Cloud Build
$ cd <FOLDER_OF_SERVICE>
$ gcloud builds submit --tag=<IMAGE_NAME> .

# deploy application
$ kubectl create deployment orders --image=<IMAGE_NAME>

# verify deployment
$ kubectl get all

# expose GKE cluster
$ kubectl expose deployment orders \
    --type="<TYPE>" \
    --port="<PORT>" \
    --target-port="<TARGET_PORT>"

# update image of cluster
$ kubectl set image <CLUSTER_NAME> <CLUSTER>=<IMAGE_NAME>

# delete the monolith service
$ kubectl delete deployment <SERVICE_NAME>
$ kubectl delete service <SERVICE_NAME>
```

- **Google Cloud Build** can be used to build the Docker container and put the image in the Container Registry.
  - The build process will take all the files from the bucket and use the Dockerfile to run the Docker build process.
  - The `--tag` flag is specified with the host as `gcr.io` for the Docker image, the resulting Docker image will be pushed to the Google Cloud Container Registry.
- Docker containers should be deployed to **Kubernetes**.
  - The [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) are smallest deployable that represent a container (or group of tightly-coupled containers)
  - The [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) is responsible for making sure the number of replicas specified are always running.

## References

- [Kubernetes](https://kubernetes.io/)
- [Deployments | Kubernetes Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Quickstart for Container Registry | Container Registry Documentation](https://cloud.google.com/container-registry/docs/quickstart)