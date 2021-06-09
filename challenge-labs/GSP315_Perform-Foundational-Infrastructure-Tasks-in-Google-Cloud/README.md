# GSP315 —— Perform Foundational Infrastructure Tasks in Google Cloud

<div align="center">
  <img src="https://i.imgur.com/F3iwIvo.png" alt="GSP313 —— Create and Manage Cloud Resources">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP315 —— Perform Foundational Infrastructure Tasks in Google Cloud](#gsp315--perform-foundational-infrastructure-tasks-in-google-cloud)
  - [Overview](#overview)
  - [Challenge Scenario](#challenge-scenario)
  - [Task 1: Create a project jumphost instance](#task-1-create-a-project-jumphost-instance)
    - [Description](#description)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console)
    - [Solution (Command Line Interface)](#solution-command-line-interface)
    - [References](#references)
  - [Task 2: Create a Kubernetes service cluster](#task-2-create-a-kubernetes-service-cluster)
    - [Description](#description-1)
    - [Solution (Command Line Interface)](#solution-command-line-interface-1)
    - [References](#references-1)
  - [Task 3: Set up an HTTP load balancer](#task-3-set-up-an-http-load-balancer)
    - [Description](#description-2)
    - [Solution (Command Line Interface)](#solution-command-line-interface-2)
    - [References](#references-2)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| Introductory | `GSP073` | [Cloud Storage: Qwik Start - Cloud Console](https://google.qwiklabs.com/focuses/1760?parent=catalog) |  |
| Introductory | `GSP074` | [Cloud Storage: Qwik Start - CLI/SDK](https://google.qwiklabs.com/focuses/569?parent=catalog) |  |
| Introductory | `GSP064` | [Cloud IAM: Qwik Start](https://google.qwiklabs.com/focuses/551?parent=catalog) | [EN](../../normal-labs/GSP064_Cloud-IAM-Qwik-Start/) |
| Introductory | `GSP089` | [Cloud Monitoring: Qwik Start](https://google.qwiklabs.com/focuses/10599?parent=catalog) | [EN](../../normal-labs/GSP089_Cloud-Monitoring-Qwik-Start/) |
| Introductory | `GSP081` | [Cloud Functions: Qwik Start - Console](https://google.qwiklabs.com/focuses/1763?parent=catalog) |  |
| Introductory | `GSP080` | [Cloud Functions: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/916?parent=catalog) |  |
| Introductory | `GSP096` | [Google Cloud Pub/Sub: Qwik Start - Console](https://google.qwiklabs.com/focuses/3719?parent=catalog) |  |
| Introductory | `GSP095` | [Google Cloud Pub/Sub: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/925?parent=catalog) |  |
| Introductory | `GSP094` | [Google Cloud Pub/Sub: Qwik Start - Python](https://google.qwiklabs.com/focuses/2775?parent=catalog) |  |
| Fundamental | `GSP315` | [Perform Foundational Infrastructure Tasks in Google Cloud: Challenge Lab](https://google.qwiklabs.com/focuses/10379?parent=catalog) |  |

</details>

## Overview

This lab is recommended for students who have enrolled in the Foundational Infrastructure Tasks in Google Cloud quest.

Topics tested:

- Create an instance
- Create a 3-node Kubernetes cluster and run a simple service
- Create an HTTP(s) load balancer in front of two web servers

## Challenge Scenario

You have started a new role as a Junior Cloud Engineer for Jooli, Inc. You are expected to help manage the infrastructure at Jooli. Common tasks include provisioning resources for projects.

You are expected to have the skills and knowledge for these tasks, so step-by-step guides are not provided.

Some Jooli, Inc. standards you should follow:

- Create all resources in the default region or zone, unless otherwise directed.
- Naming normally uses the format `team-resource`; for example, an instance could be named `nucleus-webserver1`.
- Allocate cost-effective resource sizes. Projects are monitored, and excessive resource use will result in the containing project's termination (and possibly yours), so plan carefully. This is the guidance the monitoring team is willing to share: unless directed, use `f1-micro` for small Linux VMs, and use `n1-standard-1` for Windows or other applications, such as Kubernetes nodes.

## Task 1: Create a project jumphost instance

### Description

You will use this instance to perform maintenance for the project.

**Requirements**:

- Name the instance `nucleus-jumphost`.
- Use an `f1-micro` machine type.
- Use the default image type (Debian Linux).

### Solution (Google Cloud Console)

1. **Navigation Menu** > **Compute Engine** > **VM Instance**

### Solution (Command Line Interface)

We can also use `gcloud compute instances create` command to create the Compute Engine virtual machines.

```bash
$ gcloud compute instances create nucleus-jumphost \
    --zone="us-east1-b" \
    --machine-type="f1-micro" \
    --boot-disk-size=10GB \
    --image-family="debian-10"  \
    --image-project="debian-cloud"
```

### References

- [Cloud SDK: Command Line Interface - `gcloud compute instances create`](https://cloud.google.com/sdk/gcloud/reference/compute/instances/create)

## Task 2: Create a Kubernetes service cluster

### Description

The team is building an application that will use a service running on Kubernetes. You need to:

- Create a cluster (in the `us-east1-b` zone) to host the service.
- Use the Docker container hello-app (`gcr.io/google-samples/hello-app:2.0`) as a place holder; the team will replace the container with their own work later.
- Expose the app on port `8080`.

### Solution (Command Line Interface)

The compute zone is an approximate regional location in which your clusters and their resources live. To create a cluster in the `us-east1-b` zone to host the service, you can use set the default zone for all resources then create the cluster or just create the cluster with `--zone` to specify the given zone.

```bash
# [Method 1] setup the default zone for all resources then create cluster
$ gcloud config set compute/zone us-east1-b
$ gcloud container clusters create nucleus-webserver1

# [Method 2] create cluster with specifing zone
$ gcloud container clusters create nucleus-webserver1 --zone="us-east1-b"
```

Now, we can deploy a containerized application to the cluster. Google Kubernetes Engine (GKE) uses Kubernetes objects to create and manage your cluster’s resources. Just use the Kubernetes commands `kubectl create` for creating the deployment object and `kubectl expose` for exposing apps on the given port `8080`.

```bash
# get authentication credentials for the cluster
$ gcloud container clusters get-credentials nucleus-webserver1

# create the deployment from the hello-app container image
$ kubectl create deployment hello-app --image="gcr.io/google-samples/hello-app:2.0"

# create the kubernetes service and expose to external traffic
$ kubectl expose deployment hello-app --type="LoadBalancer" --port="8080"

# [Optional] inspect the services information
$ kubectl get service
```

### References

- [Cloud SDK: Command Line Interface Documentation - `gcloud container clusters create`](https://cloud.google.com/sdk/gcloud/reference/container/clusters/create)
- [Kubernetes Documentation: create/deployment](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-deployment-em-)
- [Kubernetes Documentation: expose](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#expose)

## Task 3: Set up an HTTP load balancer

### Description

You will serve the site via nginx web servers, but you want to ensure that the environment is fault-tolerant. Create an HTTP load balancer with a managed instance group of 2 nginx web servers. Use the following code to configure the web servers; the team will replace this with their own configuration later.

```bash
$ cat << EOF > startup.sh
#! /bin/bash
apt-get update
apt-get install -y nginx
service nginx start
sed -i -- 's/nginx/Google Cloud Platform - '"\$HOSTNAME"'/' /var/www/html/index.nginx-debian.html
EOF
```

You need to:

- Create an instance template.
- Create a target pool.
- Create a managed instance group.
- Create a firewall rule to allow traffic (80/tcp).
- Create a health check.
- Create a backend service, and attach the managed instance group.
- Create a URL map, and target the HTTP proxy to route requests to your URL map.
- Create a forwarding rule.

### Solution (Command Line Interface)

1. Create an instance template:

    ```bash
    # [Method 1] create instance template with given script file
    $ cat << EOF > startup.sh
      #! /bin/bash
      apt-get update
      apt-get install -y nginx
      service nginx start
      sed -i -- 's/nginx/Google Cloud Platform - '"\$HOSTNAME"'/' /var/www/html/index.nginx-debian.html
      EOF

    $ gcloud compute instance-templates create nginx-template \
        --metadata-from-file="startup-script"="startup.sh"

    # [Method 2] create instance template directly
    $ gcloud compute instance-templates create nginx-template \
        --metadata-from-file="startup-script"="#! /bin/bash
          apt-get update
          apt-get install -y nginx
          service nginx start
          sed -i -- 's/nginx/Google Cloud Platform - '\"\$HOSTNAME\"'/' /var/www/html/index.nginx-debian.html"
    ```

2. Create a target pool:

    ```bash
    $ gcloud compute target-pools create nginx-pool
    ```

3. Create a managed instance group:

    ```bash
    $ gcloud compute instance-groups managed create nginx-group \
        --base-instance-name="nginx" \
        --size="2" \
        --template="nginx-template" \
        --target-pool="nginx-pool"

    # [Optional] check the instances list
    $ gcloud compute instances list
    ```

4. Create a firewall rule to allow traffic (80/tcp):

    ```bash
    $ gcloud compute firewall-rules create www-firewall \
        --allow="tcp:80"

    $ gcloud compute forwarding-rules create nginx-lb \
        --region="us-east1" \
        --ports="80" \
        --target-pool="nginx-pool"

    # [Optional] check the forwarding-rules list
    $ gcloud compute forwarding-rules list
    ```

5. Create a health check:

    ```bash
    $ gcloud compute http-health-checks create http-basic-check

    $ gcloud compute instance-groups managed set-named-ports nginx-group \
        --named-ports="http:80"
    ```

6. Create a backend service and attach the managed instance group:

    ```bash
    $ gcloud compute backend-services create nginx-backend \
        --protocol="HTTP" \
        --http-health-checks="http-basic-check" \
        --global

    $ gcloud compute backend-services add-backend nginx-backend \
        --instance-group="nginx-group" \
        --instance-group-zone="us-east1-b" \
        --global
    ```

7. Create a URL map and target HTTP proxy to route requests to your URL map:

    ```bash
    $ gcloud compute url-maps create web-map \
        --default-service="nginx-backend"

    $ gcloud compute target-http-proxies create http-lb-proxy \
        --url-map="web-map"
    ```

8. Create a forwarding rule:

    ```bash
    $ gcloud compute forwarding-rules create http-content-rule \
        --target-http-proxy="http-lb-proxy" \
        --ports="80" \
        --global

    # [Optional] check the forwarding-rules list
    $ gcloud compute forwarding-rules list
    ```

### References

- [`gcloud compute instance-templates create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/instance-templates/create)
- [`gcloud compute target-pools create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/target-pools/create)
- [`gcloud compute firewall-rules create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/firewall-rules/create)
- [`gcloud compute forwarding-rules create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/forwarding-rules/create)
- [`gcloud compute http-health-checks create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/http-health-checks/create)
- [`gcloud compute instance-groups managed set-named-ports` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/instance-groups/managed/set-named-ports)
- [`gcloud compute backend-services create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/backend-services/create)
- [`gcloud compute backend-services add-backend` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/backend-services/add-backend)