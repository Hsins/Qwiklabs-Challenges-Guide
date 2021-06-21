# GSP053 —— Managing Deployments Using Kubernetes Engine

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Deployments](#deployments)
- [Create Deployments](#create-deployments)
- [Scale Deployments](#scale-deployments)
- [Rolling Update](#rolling-update)
- [Canary Deployment](#canary-deployment)
- [Blue-green deployments](#blue-green-deployments)
- [References](#references)

</details>

## Overview

Dev Ops practices will regularly make use of multiple deployments to manage application deployment scenarios such as "Continuous Deployment", "Blue-Green Deployments", "Canary Deployments" and more. This lab is to provide practice in scaling and managing containers so you can accomplish these common scenarios where multiple heterogeneous deployments are being used.

## Deployments

Let's talk about **Heterogeneous deployments**, which are are called "hybrid", "multi-cloud", or "public-private", depending upon the specifics of the deployment.

- Heterogeneous deployments typically involve connecting two or more distinct infrastructure environments or regions to address a specific technical or operational need.
- Various business and technical challenges are limted to a single environment or region:
  - **Maxed out resources**: In any single environment, particularly in on-premises environments, you might not have the compute, networking, and storage resources to meet your production needs.
  - **Limited geographic reach**: Deployments in a single environment require people who are geographically distant from one another to access one deployment. Their traffic might travel around the world to a central location.
  - **Limited availability**: Web-scale traffic patterns challenge applications to remain fault-tolerant and resilient.
  - **Vendor lock-in**: Vendor-level platform and infrastructure abstractions can prevent you from porting applications.
  - **Inflexible resources**: Your resources might be limited to a particular set of compute, storage, or networking offerings.
- Heterogeneous deployments must be architected using **programmatic** and **deterministic** processes and procedures.

Three common scenarios for heterogeneous deployment are **multi-cloud deployments**, **fronting on-premises data**, and **continuous integration/continuous delivery (CI/CD)** processes.

## Create Deployments

```bash
# create deployment object
$ kubectl create --file="<FILE_PATH>"

# verify the deployment object, ReplicaSet and pods
$ kubectl get deployments
$ kubectl get replicasets
$ kubectl get pods

# check the service status
$ kubectl get services
```

## Scale Deployments

```bash
# update the replicas
$ kubectl scale deployment <SERVICE_NAME> --replicas="<NUMBER>"
```

## Rolling Update

<div align="center">
  <img src="https://i.imgur.com/m5xmRPf.png" alt="Rolling Update">
</div>

Deployments support updating images to a new version through a rolling update mechanism. When a Deployment is updated with a new version, it creates a new ReplicaSet and slowly increases the number of replicas in the new ReplicaSet as it decreases the replicas in the old ReplicaSet.

```bash
# update the deployment
$ kubectl edit deployment <SERVICE_NAME>

# check entries in rollout history
$ kubectl rollout history

# pause rolling update
$ kubectl rollout pause <SERVICE_NAME>

# resume rolling update
$ kubectl rollout resume <SERVICE_NAME>

# roll back in the history
$ kubectl rollout undo <SERVICE_NAME>

# check status of rollout
$ kubectl rollout status <SERVICE_NAME>
```

## Canary Deployment

<div align="center">
  <img src="https://i.imgur.com/6rSlQtf.png" alt="Canary Deployment">
</div>

When you want to test a new deployment in production with a subset of your users, use a canary deployment. Canary deployments allow you to release a change to a small subset of your users to mitigate risk associated with new releases. A canary deployment consists of a separate deployment with your new version and a service that targets both your normal, stable deployment as well as your canary deployment.

## Blue-green deployments

<div align="center">
  <img src="https://i.imgur.com/E5z7Qav.png" alt="Blue-green deployments">
</div>

Rolling updates are ideal because they allow you to deploy an application slowly with minimal overhead, minimal performance impact, and minimal downtime. There are instances where it is beneficial to modify the load balancers to point to that new version only after it has been fully deployed. In this case, blue-green deployments are the way to go.

Kubernetes achieves this by creating two separate deployments; one for the old "blue" version and one for the new "green" version. Use your existing deployment for the "blue" version. The deployments will be accessed via a Service which will act as the router. Once the new "green" version is up and running, you'll switch over to using that version by updating the Service.

## References

- [Six Strategies for Application Deployment | The New Stack](https://thenewstack.io/deployment-strategies/)