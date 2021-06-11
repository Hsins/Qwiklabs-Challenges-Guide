# GSP093 —— Compute Engine: Qwik Start - Windows

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

  - [Overview](#overview)
  - [Create Instance](#create-instance)
  - [Remote Desktop (RDP) into Window Server](#remote-desktop-rdp-into-window-server)
  - [References](#references)

</details>

## Overview

Compute Engine lets you create and run virtual machines on Google infrastructure. Compute Engine offers scale, performance, and value that allows you to easily launch large compute clusters on Google's infrastructure.

You can run your Windows applications on Compute Engine and take advantage of many benefits available to virtual machine instances, such as reliable [storage options](https://cloud.google.com/compute/docs/disks/), the speed of the [Google network](https://cloud.google.com/vpc/docs/vpc), and [Autoscaling](https://cloud.google.com/compute/docs/autoscaler/).

## Create Instance

1. Click **Navigation Nenu** > **Compute Engine** > **VM instances**.
2. Click **CREATE INSTANCE**.
3. Configure the instance parameters.
    - **Image**: `Windows Server 2012 R2 Datacenter`
4. Click **Create**.

## Remote Desktop (RDP) into Window Server

Before RDP into the Windows Server, we need to set password for logging.

```bash
# set password for logging
$ gcloud compute reset-windows-password <INSTANCE> \
    --zone=<ZONE> \
    --user=<USERNAME>
```

There're different ways to connect to the server through RDP:

- [Chrome RDP for Google Cloud Platform](https://chrome.google.com/webstore/detail/chrome-rdp-for-google-clo/mpbbnannobiobpnfblimoapbephgifkm)
- [CoRD](http://cord.sourceforge.net/)

## References

- [Launch a Windows Server Instance, GCP Essentials - Qwiklabs Preview | YouTube](https://www.youtube.com/watch?v=EFPaP20APuw)