# GSP319 —— Build a Website on Google Cloud

<div align="center">
  <img src="https://i.imgur.com/F3iwIvo.png" alt="GSP313 —— Create and Manage Cloud Resources">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP319 —— Build a Website on Google Cloud](#gsp319--build-a-website-on-google-cloud)
  - [Overview](#overview)
  - [Challenge Scenario](#challenge-scenario)
  - [Task 1: Download the monolith code and build your container](#task-1-download-the-monolith-code-and-build-your-container)
    - [Description](#description)
    - [Solution (Command Line Interface)](#solution-command-line-interface)
    - [References](#references)
  - [Task 2: Create a kubernetes cluster and deploy the application](#task-2-create-a-kubernetes-cluster-and-deploy-the-application)
    - [Description](#description-1)
    - [Solution (Command Line Interface)](#solution-command-line-interface-1)
    - [References](#references-1)

</details>

## Overview

This lab is recommended for students who have enrolled in the [Build a Website on Google Cloud](https://google.qwiklabs.com/quests/115) quest.

Topics tested:

- Building and refactoring a monolithic web app into microservices
- Deploying microservices in GKE
- Exposing the Services deployed on GKE

## Challenge Scenario

You have just started a new role at FancyStore, Inc.

Your task is to take the company's existing monolithic e-commerce website and break it into a series of logically separated microservices. The existing monolith code is sitting in a GitHub repo, and you will be expected to containerize this app and then refactor it.

You are expected to have the skills and knowledge for these tasks, so don't expect step-by-step guides.

You have been asked to take the lead on this, after the last team suffered from monolith-related burnout and left for greener pastures (literally, they are running a lavender farm now). You will be tasked with pulling down the source code, building a container from it (one of the farmers left you a Dockerfile), and then pushing it out to GKE.

You should first build, deploy, and test the Monolith, just to make sure that the source code is sound. After that, you should break out the constituent services into their own microservice deployments.

Some FancyStore, Inc. standards you should follow:

- Create your cluster in `us-central-1`.
- Naming is normally `team-resource`, e.g. an instance could be named `fancystore-orderservice1`.
- Allocate cost effective resource sizes. Projects are monitored and excessive resource use will result in the containing project's termination.
- Use the `n1-standard-1` machine type unless directed otherwise.

## Task 1: Download the monolith code and build your container

### Description

### Solution (Command Line Interface)

### References

## Task 2: Create a kubernetes cluster and deploy the application

### Description

### Solution (Command Line Interface)

### References