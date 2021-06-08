# GSP089 —— Cloud Monitoring: Qwik Start

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Ovewview](#ovewview)
- [Install the Monitoring and Logging Agents](#install-the-monitoring-and-logging-agents)
- [Create Monitoring workspaces](#create-monitoring-workspaces)
- [Create Uptime Check](#create-uptime-check)
- [Create Alearting Policy](#create-alearting-policy)
- [Create Dashboard](#create-dashboard)
- [View Logs](#view-logs)
- [Check Uptime Check Results and Triggered Alerts](#check-uptime-check-results-and-triggered-alerts)
- [References](#references)

</details>

## Ovewview

Cloud Monitoring provides visibility into the performance, uptime, and overall health of cloud-powered applications. Cloud Monitoring collects metrics, events, and metadata from Google Cloud, Amazon Web Services, hosted uptime probes, application instrumentation, and a variety of common application components including Cassandra, Nginx, Apache Web Server, Elasticsearch, and many others. Cloud Monitoring ingests that data and generates insights via dashboards, charts, and alerts. Cloud Monitoring alerting helps you collaborate by integrating with Slack, PagerDuty, HipChat, Campfire, and more.

## Install the Monitoring and Logging Agents

Install the Cloud Monitoring agent and Cloud Logging agent in the VMs with following commands:

```bash
# install the Cloud Monitoring agent
$ curl -sSO https://dl.google.com/cloudagents/add-monitoring-agent-repo.sh
$ sudo bash add-monitoring-agent-repo.sh
$ sudo apt-get update && sudo apt-get install stackdriver-agent -y

# install the Cloud Logging agent
$ curl -sSO https://dl.google.com/cloudagents/add-logging-agent-repo.sh
$ sudo bash add-logging-agent-repo.sh
$ sudo apt-get update && sudo apt-get install google-fluentd
```

- The **Cloud Monitoring agent** is a collectd-based daemon that gathers system and application metrics (e.g. disk, CPU, network and process metrics) from virtual machine instances and sends them to Monitoring.
- The **Cloud Logging agent** sent or stream info to Cloud Monitoring in the Cloud Console.

## Create Monitoring workspaces

Follow the steps below to create the monitoring workspace:

1. In the Cloud Console, click **Navigation menu** > **Monitoring**.
2. Wait for your workspace to be provisioned.

When the Monitoring dashboard opens, your workspace is ready.

## Create Uptime Check

Uptime checks verify that a resource is always accessible. Following the steps to create update time check of instances:

1. In the Cloud Console, click **Navigation menu** > **Monitoring** > **Uptime checks**.
2. Click **Create Uptime Check** and then fill the fields.
3. Click **Test** to verify that your uptime check can connect to the resource.
4. Click **Create** when you see a green check mark everything can connect.

## Create Alearting Policy

Use Cloud Monitoring to create one or more alerting policies:

1. In the Cloud Console, click **Navigation menu** > **Monitoring** > **Alerting**.
2. Click **Create Policy** > **Add Condition** and then fill the fields.
3. Click **Next** > **Save**.

## Create Dashboard

We can display the metrics collected by Cloud Monitoring in our own charts and dashboards. Create the charts for the lab metrics and a custom dashboard following the steps below:

1. In the Cloud Console, click **Navigation menu** > **Monitoring** > **Dashboard**.
2. Click **Create Dashboard** and then add charts.

## View Logs

Cloud Monitoring and Cloud Logging are closely integrated. Check out the logs by following steps:

1. In the Cloud Console, click **Navigation menu** > **Logging** > **Logs Explorer**.
2. Choose the logs we want to see by clicking **Resource** and then selecting resources.
3. Click **Add**.
4. Click **Stream logs**.

## Check Uptime Check Results and Triggered Alerts

- [Uptime Check] In the Cloud Console, click **Navigation menu** > **Monitoring** > **Uptime checks**.
- [Alerts] In the Cloud Console, click **Navigation menu** > **Monitoring** > **Alerting**.

## References

- [Google Cloud operations suite agents | Operations Suite Documentation](https://cloud.google.com/monitoring/agent)