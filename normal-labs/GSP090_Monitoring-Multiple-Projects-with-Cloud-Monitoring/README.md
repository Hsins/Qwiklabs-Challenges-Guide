# GSP090 —— Monitoring Multiple Projects with Cloud Monitoring

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Create Cloud Monitoring Groups](#create-cloud-monitoring-groups)
- [References](#references)

</details>

## Overview

Cloud Monitoring provides dashboards and alerts so you can review performance metrics for cloud services, virtual machines, and common open source servers such as MongoDB, Apache, Nginx, Elasticsearch, and more. You configure Cloud Monitoring in the Console.

## Create Cloud Monitoring Groups

Follow the steps below to create the Cloud Monitoring Groups:

1. In the Cloud Console, click **Navigation menu** > **Monitoring** > **Groups**.
2. Click **CREATE GROUP** and create the group. Notice the **Criteria** is a set of rules that will dynamically evaluate which resources should be part of this group.
3. Click **DONE**, then click **CREATE**.

- Cloud Monitoring lets us define and monitor groups of resources, such as VM instances, databases, and load balancers.
- Groups can be based on names, tags, regions, applications, and other criteria. We can also create subgroups, up to six levels deep, within groups.
- The Monitoring Groups can be selected in the **Applies To** field whenever we're creating monitoring such as Uptime Check.

## References

- [Google Cloud operations suite agents | Operations Suite Documentation](https://cloud.google.com/monitoring/agent)
- [Using resource groups | Operations Suite Documentation](https://cloud.google.com/monitoring/groups/)