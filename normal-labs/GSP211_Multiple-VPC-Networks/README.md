# GSP211 —— Multiple VPC Networks

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Create VPC Networks](#create-vpc-networks)
  - [Graphical User Interface](#graphical-user-interface)
  - [Command Line Interface](#command-line-interface)
- [Create the Firewall Rules](#create-the-firewall-rules)
  - [Graphical User Interface](#graphical-user-interface-1)
  - [Command Line Interface](#command-line-interface-1)
- [Create VM Instances](#create-vm-instances)
  - [Graphical User Interface](#graphical-user-interface-2)
  - [Command Line Interface](#command-line-interface-2)
- [References](#references)

</details>

## Overview

In this lab you create several VPC networks and VM instances and test connectivity across networks. Specifically, you create two custom mode networks (**managementnet** and **privatenet**) with firewall rules and VM instances as shown in this network diagram:

<div align="center">
  <img src="https://i.imgur.com/bcGqGtm.png" alt="GSP313 —— Create and Manage Cloud Resources">
</div>

The **mynetwork** network with its firewall rules and two VM instances (`mynet-eu-vm` and `mynet-us-vm`) have already been created for you in this Qwiklabs project.

## Create VPC Networks

### Graphical User Interface

1. Click **Navigation Menu** > **VPC network** > **VPC networks**.
2. Click **CREATE VPC NETWORK**.
3. Fill up the fields and click **CREATE**

### Command Line Interface

```bash
# create the network
$ gcloud compute networks create <NETWORK_NAME> --subnet-mode=custom

# create the subnets
$ gcloud compute networks subnets create <SUBNETS_NAME> \
    --region="<REGION>" \
    --network="<NETWORK_NAME>" \
    --range="<IP_RANGE>"

# list the available VPC networks
$ gcloud compute networks list

# list the available VPC subnets
$ gcloud compute networks subnets list --sort-by=NETWORK
```

## Create the Firewall Rules

### Graphical User Interface

1. Click **Navigation Menu** > **VPC network** > **Firewall**.
2. Click **CREATE FIREWALL RULE**.
3. Fill up the fields and click **CREATE**

### Command Line Interface

```bash
# create the firewall rule
$ gcloud compute firewall-rules create <FIREWALL_RULE_NAME> \
    --network="<NETWORK_NAME>" \
    --direction="<DIRECTION>" \
    --priority="<PRIORITY>" \
    --action="<ACTION>" \
    --rules="<RULES>" \
    --source-ranges="<RANGE>"

# list all the firewall rules
$ gcloud compute firewall-rules list --sort-by=NETWORK
```

## Create VM Instances

### Graphical User Interface

1. Click **Navigation Menu** > **Compute Engine** > **VM instances**.
2. Click **CREATE INSTANCE**.
3. Fill up the fields and click **CREATE**

### Command Line Interface

```bash
# create VM instances
$ gcloud compute instances create <INSTANCE_NAME> \
    --zone="<ZONE>" \
    --machine-type="<MACHINE_TYPE>" \
    --subnet="<SUBNETS_NAME>"

# list all the VM instances
$ gcloud compute instances list --sort-by=ZONE
```

## References

- [Virtual Private Cloud Documentation](https://cloud.google.com/vpc/docs)
- [`gcloud compute networks create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/networks/create)
- [`gcloud compute networks subnets create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/networks/subnets/create)
- [`gcloud compute firewall-rules create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/firewall-rules/create)