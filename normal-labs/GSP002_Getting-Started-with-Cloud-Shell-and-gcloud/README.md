# GSP002 —— Getting Started with Cloud Shell and `gcloud`

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Regions and Zones](#regions-and-zones)
- [The `gcloud` Commands](#the-gcloud-commands)
- [References](#references)

</details>

## Overview

Cloud Shell provides you with command-line access to computing resources hosted on Google Cloud. Cloud Shell is a Debian-based virtual machine with a persistent 5-GB home directory, which makes it easy for you to manage your Google Cloud projects and resources. The `gcloud` command-line tool and other utilities you need are pre-installed in Cloud Shell, which allows you to get up and running quickly.

## Regions and Zones

```bash
# check the default region and zone
$ gcloud config get-value compute/zone
$ gcloud config get-value compute/region

# check the region and zone of project
$ gcloud compute project-info describe --project <your_project_ID>
```

- Certain Google Compute Engine resources live in **regions** or **zones**.
  - **Region**: a specific geographical location where you can run your resources.
  - **Zone**: each region has one or more zones.
- Resources live in a zone are referred to as **zonal resources**. e.g. Virtual Machine
  - If you want to attach a persistent disk to a virtual machine instance, both resources must be in the same zone.
  - If you want to assign a static IP address to an instance, the instance must be in the same region as the static IP address.

## The `gcloud` Commands

```bash
# check the detailed help of commands
$ gcloud <COMMAND> --help
$ gcloud help <COMMAND>

# display the gcloud components
$ gcloud components list

# view configuration, properties and settings in environment
$ gcloud config list
$ gcloud config list --all

# enable the glcoud interactive mode
$ gcloud beta interactive
```

## References

- [Get Started with Cloud Shell, GCP Essentials - Qwiklabs Preview | YouTube](https://www.youtube.com/watch?v=ZD1zvEyfpLI)
- [Cloud SDK Documentation](https://cloud.google.com/sdk/docs)