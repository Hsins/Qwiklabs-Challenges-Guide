# GSP007 —— Set Up Network and HTTP Load Balancers

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP007 —— Set Up Network and HTTP Load Balancers](#gsp007--set-up-network-and-http-load-balancers)
  - [Overview](#overview)
  - [Network Load Balancer](#network-load-balancer)
    - [Introduction](#introduction)
    - [Example](#example)
  - [HTTP(s) Load Balancer](#https-load-balancer)
    - [Introduction](#introduction-1)
    - [Example](#example-1)
  - [References](#references)

</details>

## Overview

There are several ways you can [load balance on Google Cloud](https://cloud.google.com/load-balancing/docs/load-balancing-overview#a_closer_look_at_cloud_load_balancers):

- [Network Load Balancer](https://cloud.google.com/load-balancing/docs/network)
- [HTTP(s) Load Balancer](https://cloud.google.com/load-balancing/docs/https)

## Network Load Balancer

### Introduction

Network Load Balancer distributes external traffic among virtual machine (VM) instances **in the same region**.

- Network Load Balancer can receive traffic from any client on the internet even though the Google Cloud VMs with external IPs.
- Network Load Balancing is implemented by using [Andromeda virtual networking](https://cloud.google.com/blog/products/networking/google-cloud-networking-in-depth-how-andromeda-2-2-enables-high-throughput-vms) and [Google Maglev](https://research.google/pubs/pub44824/).
- Network load balancers are not proxies!

### Example

```bash
# create static external IP address for load balancer
$ gcloud compute addresses create <NETWORK_NAME> \
    --region=<REGION>

# add legacy health check resource
$ gcloud compute http-health-checks create <CHECK_NAME>

# add target pool in the same region
$ gcloud compute target-pools create <POOL_NAME> \
    --region=<REGION> \
    --http-health-check=<CHECK_NAME>

# add instances to the pool
$ gcloud compute target-pools add-instances <POOL_NAME> \
    --instances=<INSTANCE_NAME, ...>

# add fowarding rule
$ gcloud compute forwarding-rules create <RULE_NAME> \
    --region=<REGION> \
    --ports=<PORT> \
    --address=<NETWORK_NAME> \
    --target-pool=<POOL_NAME>
```

## HTTP(s) Load Balancer

### Introduction

Google Cloud HTTP(S) Load Balancing is a **global**, proxy-based Layer 7 load balancer that enables you to run and scale your services worldwide behind a single external IP address.

- External HTTP(S) Load Balancing distributes HTTP and HTTPS traffic to backends hosted on Compute Engine and Google Kubernetes Engine (GKE).
- External HTTP(S) Load Balancing is implemented on [Google Front Ends (GFEs)](https://cloud.google.com/security/infrastructure/design#google_front_end_service).
  - **Premium Tier**: GFEs offer cross-regional load balancing, directing traffic to the closest healthy backend that has capacity and terminating HTTP(S) traffic as close as possible to your users.
  - **Standard Tier**: the load balancing is handled regionally.

### Example

To set up a load balancer with a Compute Engine backend, your VMs need to be in an instance group. The managed instance group provides VMs running the backend servers of an external HTTP load balancer.

```bash
# create load balancer template
$ gcloud compute instance-templates create <TEMPLATE_NAME> \
    --region=<REGION> \
    --network=default \
    --subnet=default \
    --tags=<TAGS> \
    --image-family=debian-9 \
    --image-project=debian-cloud \
    --metadata=startup-script=''

# create managed instance group based on the template
$ gcloud compute instance-groups managed create <GROUP_NAME> \
    --template=<TEMPLATE_NAME> \
    --size=<SIZE> \
    --zone=<ZONE>
```

## References

- [Set Up Network & HTTP Load Balancers, GCP Essentials - Qwiklabs Preview | YouTube](https://www.youtube.com/watch?v=1ZW59HrRUzw)
- [Cloud Load Balancing Documentation](https://cloud.google.com/load-balancing/docs)