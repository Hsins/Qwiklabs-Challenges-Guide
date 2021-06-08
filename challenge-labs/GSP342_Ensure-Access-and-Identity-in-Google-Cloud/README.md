# GSP342 —— Ensure Access & Identity in Google Cloud: Challenge Lab

<div align="center">
  <img src="https://i.imgur.com/gqK7LhX.png" alt="GSP342 —— Ensure Access & Identity in Google Cloud: Challenge Lab">
</div>

- [GSP342 —— Ensure Access & Identity in Google Cloud: Challenge Lab](#gsp342--ensure-access--identity-in-google-cloud-challenge-lab)
  - [Overview](#overview)
  - [Challenge Scenario](#challenge-scenario)
  - [Your Challenge](#your-challenge)
  - [Task 1: Create a custom security role](#task-1-create-a-custom-security-role)
    - [Description](#description)
    - [Solution (Command Line Interface)](#solution-command-line-interface)
    - [References](#references)
  - [Task 2: Create a service account](#task-2-create-a-service-account)
    - [Description](#description-1)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface)
    - [Solution (Command Line Interface)](#solution-command-line-interface-1)
    - [References](#references-1)
  - [Task 3: Bind a custom security role to a service account](#task-3-bind-a-custom-security-role-to-a-service-account)
    - [Description](#description-2)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface-1)
    - [Solution (Command Line Interface)](#solution-command-line-interface-2)
    - [References](#references-2)
  - [Task 4: Create and configure a new Kubernetes Engine private cluster](#task-4-create-and-configure-a-new-kubernetes-engine-private-cluster)
    - [Description](#description-3)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface-2)
    - [Solution (Command Line Interface)](#solution-command-line-interface-3)
    - [Reference](#reference)
  - [Task 5: Deploy an application to a private Kubernetes Engine cluster.](#task-5-deploy-an-application-to-a-private-kubernetes-engine-cluster)
    - [Description](#description-4)
    - [Solution (Command Line Interface)](#solution-command-line-interface-4)
    - [References](#references-3)

## Overview

This lab is recommended for students enrolled in the [Ensure Access & Identity in Google Cloud](https://google.qwiklabs.com/quests/150) quest.

Topics tested:

- Create a custom security role.
- Create a service account.
- Bind IAM security roles to a service account.
- Create a private Kubernetes Engine cluster in a custom subnet.
- Deploy an application to a private Kubernetes Engine cluster

## Challenge Scenario

You have started a new role as a junior member of the security team for the Orca team in Jooli Inc. Your team is responsible for ensuring the security of the Cloud infrastucture and services that the company's applications depend on.

You are expected to have the skills and knowledge for these tasks, so don't expect step-by-step guides to be provided.

## Your Challenge

You have been asked to deploy, configure, and test a new Kubernetes Engine cluster that will be used for application development and pipeline testing by the the Orca development team.

As per the organisation's security standards you must ensure that the new Kubernetes Engine cluster is built according to the organisation's most recent security standards and thereby must comply with the following:

- The cluster must be deployed using a dedicated service account configured with the least privileges required.
- The cluster must be deployed as a Kubernetes Engine private cluster, with the public endpoint disabled, and the master authorized network set to include only the ip-address of the Orca group's management jumphost.
- The Kubernetes Engine private cluster must be deployed to the `orca-build-subnet` in the Orca Build VPC.

From a previous project you know that the minimum permissions required by the service account that is specified for a Kubernetes Engine cluster is covered by these three built in roles:

- `roles/monitoring.viewer`
- `roles/monitoring.metricWriter`
- `roles/logging.logWriter`

These roles are sepcified in the [documentation for hardening cluster security](https://cloud.google.com/kubernetes-engine/docs/how-to/hardening-your-cluster#use_least_privilege_sa).

You must bind the above roles to the service account used by the cluster as well as a custom role that you must create in order to provide access to any other services specified by the development team. Initially you have been told that the development team requires that the service account used by the cluster should have the permissions necessary to add and update objects in Google Cloud Storage buckets. To do this you will have to create a new custom IAM role that will provide the following permissions:

- `storage.buckets.get`
- `storage.objects.get`
- `storage.objects.list`
- `storage.objects.update`
- `storage.objects.create`

Once you have created the new private cluster you must test that it is correctly configured by connecting to it from the jumphost, `orca-jumphost`, in the management subnet `orca-mgmt-subnet`. As this compute instance is not in the same subnet as the private cluster you must make sure that the master authorized networks for the cluster includes the internal ip-address for the instance, and you must specify the `--internal-ip` flag when retrieving cluster credentials using the `gcloud container clusters get-credentials` command.

All new cloud objects and services that you create should include the "orca-" prefix.

Your final task is to validate that the cluster is working correctly by deploying a simple application to the cluster to test that management access to the cluster using the `kubectl` tool is working from the `orca-jumphost` compute instance.

## Task 1: Create a custom security role

### Description

Your first task is to create a new custom IAM security role called `orca_storage_update` that will provide the Google Cloud storage bucket and object permissions required to be able to create and update storage objects.

### Solution (Command Line Interface)

We can use the `gcloud iam roles create` command to create a new custom IAM security role and the command can be used in two ways:

- Create custom role by providing a YAML file that contains the role definition.
- Create custom role by using flags to specify the role definition.

```bash
# [Method 1] create custom role by providing a YAML file
$ cat << EOF > role-definition.yaml
title: "Orca Storage"
description: "Provide the Google Cloud storage bucket and object permissions required to be able to create and update storage objects."
includedPermissions:
- storage.buckets.get
- storage.objects.get
- storage.objects.list
- storage.objects.update
- storage.objects.create
EOF

$ gcloud iam roles create orca_storage_update \
    --project $DEVSHELL_PROJECT_ID \
    --file "role-definition.yaml"

# [Method 2] Create custom role by using flags
$ gcloud iam roles create orca_storage_update \
    --project $DEVSHELL_PROJECT_ID \
    --title "Orca Storage" \
    --description "Provide the Google Cloud storage bucket and object permissions required to be able to create and update storage objects." \
    --permissions storage.buckets.get,storage.objects.get,storage.objects.list,storage.objects.update,storage.objects.create
```

### References

- [Cloud SDK: Command Line Interface Documentation - `gcloud iam roles create`](https://cloud.google.com/sdk/gcloud/reference/iam/roles/create)
- [IAM - Creating and managing custom roles](https://cloud.google.com/iam/docs/creating-custom-roles#creating_a_custom_role)
- [Qwiklabs - GSP190: IAM Custom Roles](https://www.qwiklabs.com/focuses/1035?parent=catalog)

## Task 2: Create a service account

### Description

Your second task is to create the dedicated service account that will be used as the service account for your new private cluster. You must name this account `orca-private-cluster-sa`.

### Solution (Graphical User Interface)

1. Navigate to **IAM & Admin** in the Cloud Console
2. Click **Service Accounts** > **CREATE SERVICE ACCOUNT**.
3. Create the Service Account with name `orca-private-cluster-sa`

### Solution (Command Line Interface)

```bash
$ gcloud iam service-accounts create orca-private-cluster-sa \
   --display-name "Orca Private Cluster Service Account"
```

### References

- [Cloud SDK: Command Line Interface Documentation - `gcloud iam service-accounts create`](https://cloud.google.com/sdk/gcloud/reference/iam/service-accounts/create)
- [IAM - Creating and managing service accounts](https://cloud.google.com/iam/docs/creating-managing-service-accounts)
- [Qwiklabs - GSP199: IAM Custom Roles](https://www.qwiklabs.com/focuses/1038?parent=catalog)

## Task 3: Bind a custom security role to a service account

### Description

You must now bind the Cloud Operations logging and monitoring roles that are required for Kubernetes Engine Cluster service accounts as well as the custom IAM role you created for storage permissions to the Service Account you created earlier.

### Solution (Graphical User Interface)

1. Navigate to **IAM & Admin** in the Cloud Console
2. Click **Service Accounts** > Service Account `orca-private-cluster-sa`
3. Add roles: `orca_storage_update`, `Monitoring Viewer`, `Monitoring Metric Writer`, `Logs Writer`

### Solution (Command Line Interface)

Let's bind the built-in and custom IAM roles to the Service Account `orca-private-cluster-sa` we just created in Task 2.

```bash
# bind the required built-in roles to the service account
$ gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
    --member serviceAccount:orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com \
    --role roles/monitoring.viewer

$ gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
    --member serviceAccount:orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com \
    --role roles/monitoring.metricWriter

$ gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
    --member serviceAccount:orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com \
    --role roles/logging.logWriter

# bind the custom role orca_storage_update created previously
$ gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
    --member serviceAccount:orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com \
    --role projects/$DEVSHELL_PROJECT_ID/roles/orca_storage_update
```

### References

- [Cloud SDK: Command Line Interface Documentation - `gcloud projects add-iam-policy-binding`](https://cloud.google.com/sdk/gcloud/reference/projects/add-iam-policy-binding)
- [IAM - Granting, changing, and revoking access to resources](https://cloud.google.com/iam/docs/granting-changing-revoking-access)
- [Qwiklabs - GSP199: IAM Custom Roles](https://www.qwiklabs.com/focuses/1038?parent=catalog)

## Task 4: Create and configure a new Kubernetes Engine private cluster

### Description

You must now use the service account you have configured when creating a new Kubernetes Engine private cluster. The new cluster configuration must include the following:

- The cluster must be called `orca-test-cluster`
- The cluster must be deployed to the subnet `orca-build-subnet`
- The cluster must be configured to use the `orca-private-cluster-sa` service account.
- The private cluster options `enable-master-authorized-networks`, `enable-ip-alias`, `enable-private-nodes`, and `enable-private-endpoint` must be enabled.

Once the cluster is configured you must add the internal ip-address of the `orca-jumphost` compute instance to the master authorized network list.

### Solution (Graphical User Interface)

1. Navigate to **Compute Engine** in the Cloud Console, note down the internal IP of the `orca-jumphost` instance.
2. Navigate to **VPC network** in the Cloud Console, note down the IP range for the regional subnet. We can also lookup the IP range from [Virtual Private Cloud (VPC) - VPC network/Auto mode IP ranges](https://cloud.google.com/vpc/docs/vpc#ip-ranges).

### Solution (Command Line Interface)

We must specify a CIDR range for the VMs that run the KKubernetes master components when we create a private cluster. Let's retreive the IP range of regional subnet. (The IP range can also be lookup from [Virtual Private Cloud (VPC) - VPC network/Auto mode IP ranges](https://cloud.google.com/vpc/docs/vpc#ip-ranges))

```bash
# retrive and setup the internal IP of instance "orca-jumphost"
$ JUMPHOST_IP=$(gcloud compute instances describe orca-jumphost \
    --format='get(networkInterfaces[0].networkIP)' --zone="us-east1-b")

# retrive and setup the IP range of regional subnet
$ SUBNET_IP_RANGE="10.142.0.0/28"

# [Optional] view our subnet and secondary address ranges
$ gcloud compute networks subnets list --network default
$ gcloud compute networks subnets describe [SUBNET_NAME] --region us-central1
```

With the internal IP of instace `orca-jumphost` and the IP range of regional subnet, we can create the private cluster named `orca-test-cluster` for the masters.

```bash
$ gcloud container clusters create orca-test-cluster \
    --zone "us-east1-b" \
    --network "orca-build-vpc" \
    --subnetwork "orca-build-subnet" \
    --master-ipv4-cidr $SUBNET_IP_RANGE \
    --master-authorized-networks $JUMPHOST_IP/32 \
    --enable-master-authorized-networks \
    --enable-ip-alias \
    --enable-private-nodes \
    --enable-private-endpoint \
    --service-account orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com
```

### Reference

- [Cloud SDK: Command Line Interface Documentation - `gcloud container clusters create`](https://cloud.google.com/sdk/gcloud/reference/container/clusters/create)
- [IAM - Granting, changing, and revoking access to resources](https://cloud.google.com/iam/docs/granting-changing-revoking-access)
- [Virtual Private Cloud (VPC) - VPC network overview](https://cloud.google.com/vpc/docs/vpc)
- [Qwiklabs - GSP178: Setting up a Private Kubernetes Cluster](https://www.qwiklabs.com/focuses/867?parent=catalog)

## Task 5: Deploy an application to a private Kubernetes Engine cluster.

### Description

You have a simple test application that can be deployed to any cluster to quickly test that basic container deployment functionality is working and that basic services can be created and accessed. You must configure the environment so that you can deploy this simple demo to the new cluster using the jumphost `orca-jumphost`.

```bash
$ kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
```

This deploys an application that listens on port `8080` that can be exposed using a basic load balancer service for testing.

### Solution (Command Line Interface)

To deploy an application to the Kubernetes Engine cluster, we should use SSH to connect the source-instance since the Cloud Shell cannot directly access the private cluster.

```bash
# use SSH connect into the source-instance
$ gcloud compute ssh orca-jumphost \
    --zone "us-east1-b" \
    --project $DEVSHELL_PROJECT_ID
```

Kubernetes provides the Deployment object for deploying stateless applications like web servers. We can just use the `kubectl` command to create a deployment object that represents `hello-server`.

```bash
# get authentication credentials for the cluster
$ gcloud container clusters get-credentials orca-test-cluster \
    --internal-ip \
    --zone "us-east1-b"

# create a new Deployment hello-server from the hello-app container image
$ kubectl create deployment hello-server \
    --image "gcr.io/google-samples/hello-app:1.0"

# [Optional] create a Kubernetes Service exposing application to external traffic
$ kubectl expose deployment hello-server \
    --name orca-hello-service \
    --type LoadBalancer \
    --port 80 --target-port 8080
```

### References

- [Cloud SDK: Command Line Interface Documentation - `gcloud container clusters create`](https://cloud.google.com/sdk/gcloud/reference/container/clusters/create)
- [Google Kubernetes Engine (GKE) - Exposing applications using services](https://cloud.google.com/kubernetes-engine/docs/how-to/exposing-apps)
- [Qwiklabs - GSP178: Setting up a Private Kubernetes Cluster](https://www.qwiklabs.com/focuses/867?parent=catalog)