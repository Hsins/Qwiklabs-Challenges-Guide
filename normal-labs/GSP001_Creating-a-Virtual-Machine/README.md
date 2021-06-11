# GSP001 —— Creating a Virtual Machine

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Create Instance (Graphical User Interface)](#create-instance-graphical-user-interface)
- [Create Instance (Command Line Interface)](#create-instance-command-line-interface)
- [References](#references)

</details>

## Overview

Compute Engine lets you create virtual machines that run different operating systems, including multiple flavors of Linux (Debian, Ubuntu, Suse, Red Hat, CoreOS) and Windows Server, on Google infrastructure. You can run thousands of virtual CPUs on a system that is designed to be fast and to offer strong consistency of performance.

## Create Instance (Graphical User Interface)

1. Click **Navigation Menu** > **Compute Engine** > **VM Instances**.
2. Click **CREATE INSTANCE**.
3. Configure the instance parameters.
4. Click **CREATE**

## Create Instance (Command Line Interface)

```bash
$ gcloud compute instances create <NAME> \
    --zone=<ZONE> \
    --machine-type=<MACHINE_TYPE> \
```

## References

- [Create a Virtual Machine, GCP Essentials - Qwiklabs Preview | YouTube](https://www.youtube.com/watch?v=ew-r46FmzSM)
- [`gcloud` command-line tool overview | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/)