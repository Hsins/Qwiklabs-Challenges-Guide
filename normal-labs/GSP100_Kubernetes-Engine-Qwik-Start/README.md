# GSP100 —— Kubernetes Engine: Qwik Start

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Google Kubernetes Engine](#google-kubernetes-engine)
- [Manipulate GKE Cluster](#manipulate-gke-cluster)
- [References](#references)

</details>

## Overview

[Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine/) (GKE) provides a managed environment for deploying, managing, and scaling your containerized applications using Google infrastructure. The Kubernetes Engine environment consists of multiple machines (specifically [Compute Engine](https://cloud.google.com/compute) instances) grouped to form a [container cluster](https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-architecture). In this lab, you get hands-on practice with container creation and application deployment with GKE.

## Google Kubernetes Engine

Google Kubernetes Engine (GKE) clusters are powered by the Kubernetes open source cluster management system. Kubernetes provides the mechanisms through which you interact with your container cluster.

- A **cluster** consists of at least one cluster master machine and multiple worker machines called nodes.
- **Nodes** are Compute Engine virtual machine (VM) instances that run the Kubernetes processes necessary to make them part of the cluster.

The benefit of Google Kubernetes Engine (GKE) cluster:

- [Load Balancing](https://cloud.google.com/compute/docs/load-balancing-and-autoscaling): distribute incoming traffic across multiple virtual machine (VM) instances
- [Node Pools](https://cloud.google.com/kubernetes-engine/docs/concepts/node-pools): designate subsets of nodes within a cluster that all have the same configuration for additional flexibility
- [Automatic Scale](https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-autoscaler): automatically resizes the number of nodes in a given node pool, based on the demands of your workloads
- [Automatic Upgrade](https://cloud.google.com/kubernetes-engine/docs/how-to/node-auto-upgrades): keep the nodes in cluster up-to-date with the cluster control plane (master) version when the control plane is updated on our behalf
- [Node auto-repair](https://cloud.google.com/kubernetes-engine/docs/how-to/node-auto-repair): makes periodic checks on the health state of each node in your cluster to keep nodes in a healthy and running state

## Manipulate GKE Cluster

```bash
# create cluster
$ gcloud container clusters create <CLUSTER-NAME>

# authenticate cluster
$ gcloud container clusters get-credentials <CLUSTER-NAME>

# deploy containerized application
$ kubectl create deployment hello-server --image=<IMAGE>
$ kubectl expose deployment hello-server --type=<TYPE> --port=<PORT>

# delete cluster
$ gcloud container clusters delete <CLUSTER-NAME>
```

- GKE uses Kubernetes objects to create and manage the cluster's resources.
- Kubernetes provides:
  - [Deployment object](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) for deploying stateless applications.
  - [Service objects](https://kubernetes.io/docs/concepts/services-networking/service/) define rules and load balancing for accessing application from the internet.

## References

- [Manage Containerized Apps with Kubernetes Engine | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=u9nsngvmMK4)
- [Google Kubernetes Engine Documentation](https://cloud.google.com/kubernetes-engine/docs)