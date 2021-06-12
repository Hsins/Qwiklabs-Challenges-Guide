# GSP321 —— Set Up and Configure a Cloud Environment in Google Cloud

<div align="center">
  <img src="https://i.imgur.com/F3iwIvo.png" alt="GSP313 —— Create and Manage Cloud Resources">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP321 —— Set Up and Configure a Cloud Environment in Google Cloud](#gsp321--set-up-and-configure-a-cloud-environment-in-google-cloud)
  - [Overview](#overview)
  - [Challenge Scenario](#challenge-scenario)
  - [Your Challenge](#your-challenge)
  - [Task 1: Create development VPC manually](#task-1-create-development-vpc-manually)
    - [Description](#description)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console)
    - [Solution (Command Line Interface)](#solution-command-line-interface)
    - [References](#references)
  - [Task 2: Create production VPC manually](#task-2-create-production-vpc-manually)
    - [Description](#description-1)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-1)
    - [Solution (Command Line Interface)](#solution-command-line-interface-1)
    - [References](#references-1)
  - [Task 3: Create bastion host](#task-3-create-bastion-host)
    - [Description](#description-2)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-2)
    - [Solution (Command Line Interface)](#solution-command-line-interface-2)
    - [References](#references-2)
  - [Task 4: Create and configure Cloud SQL Instance](#task-4-create-and-configure-cloud-sql-instance)
    - [Description](#description-3)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-3)
    - [Solution (Command Line Interface)](#solution-command-line-interface-3)
    - [References](#references-3)
  - [Task 5: Create Kubernetes cluster](#task-5-create-kubernetes-cluster)
    - [Description](#description-4)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-4)
    - [Solution (Command Line Interface)](#solution-command-line-interface-4)
    - [References](#references-4)
  - [Task 6: Prepare the Kubernetes cluster](#task-6-prepare-the-kubernetes-cluster)
    - [Description](#description-5)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-5)
    - [Solution (Command Line Interface)](#solution-command-line-interface-5)
    - [References](#references-5)
  - [Task 7: Create a WordPress deployment](#task-7-create-a-wordpress-deployment)
    - [Description](#description-6)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-6)
    - [Solution (Command Line Interface)](#solution-command-line-interface-6)
    - [References](#references-6)
  - [Task 8: Enable monitoring](#task-8-enable-monitoring)
    - [Description](#description-7)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-7)
    - [Solution (Command Line Interface)](#solution-command-line-interface-7)
    - [References](#references-7)
  - [Task 9: Provide access for an additional engineer](#task-9-provide-access-for-an-additional-engineer)
    - [Description](#description-8)
    - [Solution (Google Cloud Console)](#solution-google-cloud-console-8)
    - [Solution (Command Line Interface)](#solution-command-line-interface-8)
    - [References](#references-8)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| Introductory | `GSP064` | [Cloud IAM: Qwik Start](https://google.qwiklabs.com/focuses/551?parent=catalog) | [EN](../../normal-labs/GSP064_Cloud-IAM-Qwik-Start/) |
| Introductory | `GSP281` | [Introduction to SQL for BigQuery and Cloud SQL](https://google.qwiklabs.com/focuses/2802?parent=catalog) | [EN](./normal-labs/GSP281_Introduction-to-SQL-for-BigQuery-and-Cloud-SQL/) |
| Advanced | `GSP211` | [Multiple VPC Networks](https://google.qwiklabs.com/focuses/1230?parent=catalog) |  |
| Introductory | `GSP089` | [Cloud Monitoring: Qwik Start](https://google.qwiklabs.com/focuses/10599?parent=catalog) | [EN](../../normal-labs/GSP089_Cloud-Monitoring-Qwik-Start/) |
| Advanced | `GSP053` | [Managing Deployments Using Kubernetes Engine](https://google.qwiklabs.com/focuses/639?parent=catalog) |  |
| Expert | `GSP321` | [Set Up and Configure a Cloud Environment in Google Cloud: Challenge Lab](https://google.qwiklabs.com/focuses/10603?parent=catalog) |  |

</details>

## Overview

This lab is only recommended for students who have completed the labs in the [Set up and Configure a Cloud Environment in Google Cloud](https://google.qwiklabs.com/quests/119) quest.

Topics tested:

- Creating and using VPCs and subnets
- Creating a Kubernetes cluster
- Configuring and launching a Kubernetes deployment and service
- Setting up stackdriver monitoring
- Configuring an IAM role for an account

## Challenge Scenario

As a cloud engineer in Jooli Inc. and recently trained with Google Cloud and Kubernetes you have been asked to help a new team (Griffin) set up their environment. The team has asked for your help and has done some work, but needs you to complete the work.

You are expected to have the skills and knowledge for these tasks so don’t expect step-by-step guides.

You need to complete the following tasks:

- Create a development VPC with three subnets manually
- Create a production VPC with three subnets manually
- Create a bastion that is connected to both VPCs
- Create a development Cloud SQL Instance and connect and prepare the WordPress environment
- Create a Kubernetes cluster in the development VPC for WordPress
- Prepare the Kubernetes cluster for the WordPress environment
- Create a WordPress deployment using the supplied configuration
- Enable monitoring of the cluster via stackdriver
- Provide access for an additional engineer

Some Jooli Inc. standards you should follow:

- Create all resources in the `us-east1` region and `us-east1-b` zone, unless otherwise directed.
- Use the project VPCs.
- Naming is normally `team-resource`, e.g. an instance could be named `kraken-webserver1`.
- Allocate cost effective resource sizes. Projects are monitored and excessive resource use will result in the containing project's termination (and possibly yours), so beware. This is the guidance the monitoring team is willing to share: unless directed, use `n1-standard-1`.

## Your Challenge

You need to help the team with some of their initial work on a new project. They plan to use WordPress and need you to set up a development environment. Some of the work was already done for you, but other parts require your expert skills.

As soon as you sit down at your desk and open your new laptop you receive the following request to complete these tasks. Good luck!

## Task 1: Create development VPC manually

### Description

Create a VPC called `griffin-dev-vpc` with the following subnets only:

- `griffin-dev-wp`
    - IP address block: `192.168.16.0/20`
- `griffin-dev-mgmt`
    - IP address block: `192.168.32.0/20`

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Task 2: Create production VPC manually

### Description

Create a VPC called `griffin-prod-vpc` with the following subnets only:

- `griffin-prod-wp`
    - IP address block: `192.168.48.0/20`
- `griffin-prod-mgmt`
    - IP address block: `192.168.64.0/20`

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Task 3: Create bastion host

### Description

Create a bastion host with two network interfaces, one connected to `griffin-dev-mgmt` and the other connected to `griffin-prod-mgmt`. Make sure you can SSH to the host.

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Task 4: Create and configure Cloud SQL Instance

### Description

Create a **MySQL Cloud SQL Instance** called `griffin-dev-db` in `us-east1`. Connect to the instance and run the following SQL commands to prepare the **WordPress** environment:

```sql
CREATE DATABASE wordpress;
GRANT ALL PRIVILEGES ON wordpress.* TO "wp_user"@"%" IDENTIFIED BY "stormwind_rules";
FLUSH PRIVILEGES;
```

These SQL statements create the worpdress database and create a user with access to the wordpress database. You will use the username and password in task 6.

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Task 5: Create Kubernetes cluster

### Description

Create a 2 node cluster (`n1-standard-4`) called `griffin-dev`, in the `griffin-dev-wp` subnet, and in zone `us-east1-b`.

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Task 6: Prepare the Kubernetes cluster

### Description

Use Cloud Shell and copy all files from `gs://cloud-training/gsp321/wp-k8s`.

The **WordPress** server needs to access the MySQL database using the username and password you created in task 4. You do this by setting the values as secrets. **WordPress** also needs to store its working files outside the container, so you need to create a volume.

Add the following secrets and volume to the cluster using `wp-env.yaml`. Make sure you configure the username to `wp_user` and password to `stormwind_rules` before creating the configuration.

You also need to provide a key for a service account that was already set up. This service account provides access to the database for a sidecar container. Use the command below to create the key, and then add the key to the Kubernetes environment.

```bash
$ gcloud iam service-accounts keys create key.json \
    --iam-account="cloud-sql-proxy@$GOOGLE_CLOUD_PROJECT.iam.gserviceaccount.com"
$ kubectl create secret generic cloudsql-instance-credentials \
    --from-file="key.json"
```

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Task 7: Create a WordPress deployment

### Description

Now you have provisioned the MySQL database, and set up the secrets and volume, you can create the deployment using `wp-deployment.yaml`. Before you create the deployment you need to edit `wp-deployment.yaml` and replace `YOUR_SQL_INSTANCE` with `griffin-dev-db`'s Instance connection name. Get the Instance connection name from your Cloud SQL instance.

After you create your WordPress deployment, create the service with `wp-service.yaml`.

Once the Load Balancer is created, you can visit the site and ensure you see the **WordPress** site installer. At this point the dev team will take over and complete the install and you move on to the next task.

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Task 8: Enable monitoring

### Description

Create an uptime check for your WordPress development site.

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References

## Task 9: Provide access for an additional engineer

### Description

You have an additional engineer starting and you want to ensure they have access to the project, so please go ahead and grant them the editor role to the project.

The second user account for the lab represents the additional engineer.

### Solution (Google Cloud Console)

### Solution (Command Line Interface)

### References