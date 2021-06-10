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
  - [Your challenge](#your-challenge)
  - [Task 1: Create a bucket](#task-1-create-a-bucket)
    - [Description](#description)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface)
    - [Solution (Command Line Interface)](#solution-command-line-interface)
    - [References](#references)
  - [Task 2: Create a Pub/Sub topic](#task-2-create-a-pubsub-topic)
    - [Description](#description-1)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface-1)
    - [Solution (Command Line Interface)](#solution-command-line-interface-1)
    - [References](#references-1)
  - [Task 3: Create the thumbnail Cloud Function](#task-3-create-the-thumbnail-cloud-function)
    - [Description](#description-2)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface-2)
    - [Solution (Command Line Interface)](#solution-command-line-interface-2)
    - [References](#references-2)
  - [Task 4: Remove the previous cloud engineer](#task-4-remove-the-previous-cloud-engineer)
    - [Description](#description-3)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface-3)
    - [Solution (Command Line Interface)](#solution-command-line-interface-3)
    - [References](#references-3)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| Introductory | `GSP073` | [Cloud Storage: Qwik Start - Cloud Console](https://google.qwiklabs.com/focuses/1760?parent=catalog) | [EN](../../normal-labs/GSP073_Cloud-Storage-Qwik-Start-Cloud-Console/) |
| Introductory | `GSP074` | [Cloud Storage: Qwik Start - CLI/SDK](https://google.qwiklabs.com/focuses/569?parent=catalog) | [EN](../../normal-labs/GSP074_Cloud-Storage-Qwik-Start-CLI-SDK/) |
| Introductory | `GSP064` | [Cloud IAM: Qwik Start](https://google.qwiklabs.com/focuses/551?parent=catalog) | [EN](../../normal-labs/GSP064_Cloud-IAM-Qwik-Start/) |
| Introductory | `GSP089` | [Cloud Monitoring: Qwik Start](https://google.qwiklabs.com/focuses/10599?parent=catalog) | [EN](../../normal-labs/GSP089_Cloud-Monitoring-Qwik-Start/) |
| Introductory | `GSP081` | [Cloud Functions: Qwik Start - Console](https://google.qwiklabs.com/focuses/1763?parent=catalog) | [EN](../../normal-labs/GSP081_Cloud-Functions-Qwik-Start-Console/) |
| Introductory | `GSP080` | [Cloud Functions: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/916?parent=catalog) | [EN](../../normal-labs/GSP080_Cloud-Functions-Qwik-Start-Command-Line/) |
| Introductory | `GSP096` | [Google Cloud Pub/Sub: Qwik Start - Console](https://google.qwiklabs.com/focuses/3719?parent=catalog) |  |
| Introductory | `GSP095` | [Google Cloud Pub/Sub: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/925?parent=catalog) |  |
| Introductory | `GSP094` | [Google Cloud Pub/Sub: Qwik Start - Python](https://google.qwiklabs.com/focuses/2775?parent=catalog) |  |
| Fundamental | `GSP315` | [Perform Foundational Infrastructure Tasks in Google Cloud: Challenge Lab](https://google.qwiklabs.com/focuses/10379?parent=catalog) |  |

</details>

## Overview

This lab is recommended for students who have enrolled in the [Foundational Infrastructure Tasks in Google Cloud](https://google.qwiklabs.com/quests/118) quest.

## Challenge Scenario

You are just starting your junior cloud engineer role with Jooli inc. So far you have been helping teams create and manage Google Cloud resources.

You are expected to have the skills and knowledge for these tasks so don’t expect step-by-step guides.

## Your challenge

You are now asked to help a newly formed development team with some of their initial work on a new project around storing and organizing photographs, called memories. You have been asked to assist the memories team with initial configuration for their application development environment; you receive the following request to complete the following tasks:

- Create a bucket for storing the photographs.
- Create a Pub/Sub topic that will be used by a Cloud Function you create.
- Create a Cloud Function.
- Remove the previous cloud engineer’s access from the memories project.

Some Jooli Inc. standards you should follow:

- Create all resources in the `us-east1` region and `us-east1-b` zone, unless otherwise directed.
- Use the project VPCs.
- Naming is normally `team-resource`, e.g. an instance could be named `kraken-webserver1`
- Allocate cost effective resource sizes. Projects are monitored and excessive resource use will result in the containing project's termination (and possibly yours), so beware. This is the guidance the monitoring team is willing to share; unless directed, use `f1-micro` for small Linux VMs and `n1-standard-1` for Windows or other applications such as Kubernetes nodes.

## Task 1: Create a bucket

### Description

You need to create a bucket for the storage of the photographs.

### Solution (Graphical User Interface)

### Solution (Command Line Interface)

### References

## Task 2: Create a Pub/Sub topic

### Description

Create a Pub/Sub topic for the Cloud Function to send messages.

### Solution (Graphical User Interface)

### Solution (Command Line Interface)

### References

## Task 3: Create the thumbnail Cloud Function

### Description

Create a Cloud Function that executes every time an object is created in the bucket you created in task 1. The function is written in Node.js 10. Make sure you set the **Entry point** (Function to execute) to `thumbnail` and **Trigger** to `Cloud Storage`.

> You must upload one JPG or PNG image into the bucket, we will verify the thumbnail was created (after creating the function successfully). Use any JPG or PNG image, or use this [image](https://storage.googleapis.com/cloud-training/gsp315/map.jpg); download the image to your machine and then upload that file to your bucket. You will see a thumbnail image appear shortly afterwards (use **REFRESH** in the bucket details).

### Solution (Graphical User Interface)

### Solution (Command Line Interface)

### References

## Task 4: Remove the previous cloud engineer

### Description

You will see that there are two users, one is your account (with the role of Owner) and the other is the previous cloud engineer (with the role of Viewer). We like to keep our security tight, so please remove the previous cloud engineer’s access to the project.

### Solution (Graphical User Interface)

### Solution (Command Line Interface)

### References
