# GSP338 —— Monitor and Log with Google Cloud Operations Suite

<div align="center">
  <img src="https://i.imgur.com/pXwuLP9.png" alt="GSP338 —— Monitor and Log with Google Cloud Operations Suite">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Challenge Scenario](#challenge-scenario)
- [Your Challenge](#your-challenge)
- [Task 1: Configure Cloud Monitoring](#task-1-configure-cloud-monitoring)
  - [Description](#description)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface)
  - [References](#references)
- [Task 2: Configure a Compute Instance to generate Custom Cloud Monitoring metrics](#task-2-configure-a-compute-instance-to-generate-custom-cloud-monitoring-metrics)
  - [Description](#description-1)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface-1)
  - [Solution (Command Line Interface)](#solution-command-line-interface)
  - [References](#references-1)
- [Task 3: Create a custom metric using Cloud Operations logging events](#task-3-create-a-custom-metric-using-cloud-operations-logging-events)
  - [Description](#description-2)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface-2)
  - [References](#references-2)
- [Task 4: Add custom metrics to the Media Dashboard in Cloud Operations Monitoring](#task-4-add-custom-metrics-to-the-media-dashboard-in-cloud-operations-monitoring)
  - [Description](#description-3)
  - [Solution (Graphical User Interface): Monitoring/Dashboards](#solution-graphical-user-interface-monitoringdashboards)
  - [Solution (Graphical User Interface): Monitoring/Metrics Explorer](#solution-graphical-user-interface-monitoringmetrics-explorer)
  - [Reference](#reference)
- [Task 5: Create a Cloud Operations alert based on the rate of high resolution video file uploads](#task-5-create-a-cloud-operations-alert-based-on-the-rate-of-high-resolution-video-file-uploads)
  - [Description](#description-4)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface-3)
  - [Solution (Command Line Interface)](#solution-command-line-interface-1)
  - [References](#references-3)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| Introductory | `GSP089` | [Cloud Monitoring: Qwik Start](https://google.qwiklabs.com/focuses/10599?parent=catalog) | [EN](../../normal-labs/GSP089_Cloud-Monitoring-Qwik-Start/) |
| Fundamental | `GSP090` | [Monitoring Multiple Projects with Cloud Monitoring](https://google.qwiklabs.com/focuses/10621?parent=catalog) | [EN](../../normal-labs/GSP090_Monitoring-Multiple-Projects-with-Cloud-Monitoring/) |
| Fundamental | `GSP092` | [Monitoring and Logging for Cloud Functions](https://google.qwiklabs.com/focuses/1833?parent=catalog) | [EN](../../normal-labs/GSP092_Monitoring-and-Logging-for-Cloud-Functions/) |
| Fundamental | `GSP111` | [Reporting Application Metrics into Cloud Monitoring](https://google.qwiklabs.com/focuses/1259?parent=catalog) | [EN](../../normal-labs/GSP111_Reporting-Application-Metrics-into-Cloud-Monitoring/) |
| Advanced | `GSP091` | [Creating and Alerting on Logs-based Metrics](https://google.qwiklabs.com/focuses/619?parent=catalog) | [EN](../../normal-labs/GSP091_Creating-and-Alerting-on-Logs-based-Metrics/) |
| Advanced | `GSP087` | [Autoscaling an Instance Group with Custom Cloud Monitoring Metrics](https://google.qwiklabs.com/focuses/611?parent=catalog) | [EN](../../normal-labs/GSP087_Autoscaling-an-Instance-Group-with-Custom-Cloud-Monitoring-Metrics/)|
| Expert | `GSP338` | [Monitor and Log with Google Cloud Operations Suite: Challenge Lab](https://google.qwiklabs.com/focuses/13786?parent=catalog) |  |

</details>

## Overview

This lab is recommended for students enrolled in the [Monitor and Log with Google Cloud Operations Suite](https://google.qwiklabs.com/quests/143) Quest.

Topics tested:

- Initialize Cloud Monitoring.
- Configure a Compute Engine application for Cloud Operations Monitoring custom metrics.
- Create a custom metric using Cloud Operations logging events.
- Add custom metrics to a Cloud Monitoring Dashboard.
- Create a Cloud Operations alert.

## Challenge Scenario

In your new role as Junior Cloud Engineer for Jooli Inc., you're expected to help manage the Cloud infrastructure components and support the video operations team. Common tasks include monitoring resource utilization, analyzing logs, configuring alerts, and reporting on any issues related to Jooli Inc.'s online services.

As you're expected to have the skills and knowledge for these tasks, step-by-step guides are not provided.

Some Jooli Inc. standards you should follow:

- Create all resources in the `us-east1` region and `us-east1-b` zone, unless otherwise directed.
- Naming is `team-resource`, e.g. an instance could be named `video-webserver1`.
- Allocate cost effective resource sizes. Projects are monitored and excessive resource use will result in the containing project's termination (and possibly yours), so beware. Unless directed, use `n1-standard-1`.

## Your Challenge

On the first day of your new job, your manager gives you a series of tasks that you must complete. Good luck!

Your primary concern is a media upload function that Jooli Inc. provides. This function allows subscribers to upload video content to edit and transform using Jooli Inc.'s innovative range of cloud based media production tools.

The media upload function is a critical part of the service, and it is vital that Jooli Inc. is aware of any changes in the behavior of the users that might impact performance or cost of the services.

Your tasks today will use Cloud Operations tools to improve the company's ability to identify such changes and respond to them rapidly. Your manager has told you that the company is concerned that recent changes in end user behavior, combined with a new generation of phones and tablets, is fuelling a demand for much higher media such as 4K, and even 8K, video. Storage for the data is a relatively minor concern but the company wants to make sure that resource consumption by the Cloud Functions used for media upload and transcoding do not run into any limits or result in unexpected spikes in billing costs.

## Task 1: Configure Cloud Monitoring

### Description

Your first task is to enable Cloud Monitoring for your project.

A basic Cloud Monitoring dashboard, called **Media_Dashboard**, will be made available to you automatically, but you have to enable Cloud Monitoring in your project before you will be able to access this dashboard.

Once you initialize Cloud Monitoring, you can access the initial dashboard, called **Media_Dashboard**. In subsequent tasks you will add custom metrics to this basic dashboard. The initial dashboard configuration incldues some charts that display stats about the latency of the video upload Cloud Function.

### Solution (Graphical User Interface)

1. Navigate to **Navigation menu** > **Monitoring**.
2. Wait for the workspace to be provisioned.

### References

- [Cloud Monitoring: Qwik Start | Qwiklabs](https://google.qwiklabs.com/focuses/10599?parent=catalog)

## Task 2: Configure a Compute Instance to generate Custom Cloud Monitoring metrics

### Description

Your next task is to confirm that the monitoring service that checks the length of the video processing queue is working correctly.

The monitoring service creates a custom metric, `opencensus/my.videoservice.org/measure/input_queue_size`, that allows you to monitor the state of the Jooli Inc.'s video processing queue. This custom metric is created and written to by a Go application that runs on a Compute Instance called `video-queue-monitor`.

The `video-queue-monitor` Compute Instance has been deployed for you and uses a startup script to install and launch the input queue monitoring Go application. This application was tested fully in a development environment but the configuration in your Compute Instance has not been finalized. The Go application will not write custom metric data until the application is correctly configured by the startup script.

You must modify the startup script for the `video-queue-monitor` Compute Instance so that the queue monitoring application (the Go application) can create and write to custom metrics. Once you have updated the startup script you will need to restart the instance.

The Go application is installed in the `/work/go` directory in the Compute Instance by the startup script.

You can confirm that the application is working by searching for the metric `input_queue_size` in the Metrics Explorer in Cloud Monitoring.

### Solution (Graphical User Interface)

1. In the Cloud Console, click **Navigation Menu** > **Compute Engine** > **VM Instances**.
2. Click the instance named `video-queue-monitor`.
3. Click **EDIT**
4. Modify the value of of `startup-script` in **Custom metadata**.

  ```bash
    ...
  # Configure env vars for the Video Queue processing application
  export MY_PROJECT_ID=<PROJECT_ID>
  export MY_GCE_INSTANCE_ID=<INSTANCE-ID>
  export MY_GCE_INSTANCE_ZONE="us-east1-b"
    ...
  ```
5. Click **Save**
6. Go back to **Stop** and then **Start** the instance `video-queue-monitor`.

### Solution (Command Line Interface)

The startup script for the Compute Instance is in the Compute Instance metadata key called `startup_script`. We can use `gcloud compute instances add-metadata` command for [updating metadata on a running instance](https://cloud.google.com/compute/docs/storing-retrieving-metadata#update_metadata).

```bash
# setup the environment variables
$ PROJECT_ID=$DEVSHELL_PROJECT_ID
$ INSTANCE_ID=$(gcloud compute instances describe "video-queue-monitor" --zone="us-east1-b" --format="value[](id)")
$ INSTANCE_ZONE="us-east1-b"

# retrieve the original start-script.sh and replace content with environment variables
$ gcloud compute instances describe "video-queue-monitor" \
    --zone="us-east1-b" \
    --format="value[](metadata.items.startup-script)" \
    > "start-script.sh"

$ sed "s/\[REPLACE-WITH-PROJECT_ID\]/$PROJECT_ID/g" -i start-script.sh
$ sed "s/\[REPLACE-WITH-INSTANCE-ID\]/$INSTANCE_ID/g" -i start-script.sh
$ sed "s/\[REPLACE-WITH-INSTANCE-ZONE\]/$INSTANCE_ZONE/g" -i start-script.sh

# update the metadata
$ gcloud compute instances add-metadata "video-queue-monitor" \
    --zone="us-east1-b" \
    --metadata-from-file="startup_script"="start-script.sh"
```

Don't forget to restart the instance once we have updated the startup script.

```bash
# restart the instance
$ gcloud compute instances stop "video-queue-monitor" --zone="us-east1-b"
$ gcloud compute instances start "video-queue-monitor" --zone="us-east1-b"
```

### References

- [`gcloud compute instances add-metadata` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/compute/instances/add-metadata)
- [Stopping and starting a VM | Compute Engine Documentation](https://cloud.google.com/compute/docs/instances/stop-start-instance)

## Task 3: Create a custom metric using Cloud Operations logging events

### Description

Examine the Cloud Operations logs and create a custom metric that tracks the total volume of uploaded media files to your Cloud Function. The video upload Cloud Function creates a Cloud Operations Logging event that includes metadata about the type of video file the video processing system handles. You have been asked to configure a custom log based metric called `large_video_upload_rate` that will monitor the rate at which high resolution video files, those recorded at either 4K or 8K resolution, are uploaded. The Cloud Function is already processing this data, and if you search the Cloud Operations logs using the advanced filter mode you will find log entries that contain the string `"file_format: 4K"` or `"file_format: 8K"` in the `textPayload` field whenever the `video_processing` Cloud Function receives a request to process a high resolution video. You can use that filter to create your custom metric.

### Solution (Graphical User Interface)

1. In the Cloud Console, click **Navigation menu** > **Logging** > **Logs Explorer**.
2. Use the query criteria `textPayload=~"file_format\: ([4,8]K).*"` and then click **Run Query**.
3. On top right of the **Query Results** section, click **Actions** drop down and select **Create Metric**.
4. Create the custom metric with the name `large_video_upload_rate`.

### References

- [Creating and Alerting on Logs-based Metrics | Qwiklabs](https://google.qwiklabs.com/focuses/619?parent=catalog)
- [Creating custom metrics | Cloud Monitoring Document](https://cloud.google.com/monitoring/custom-metrics/creating-metrics)

## Task 4: Add custom metrics to the Media Dashboard in Cloud Operations Monitoring

### Description

You must now add two charts to the Media Dashboard:

1. Add a chart for the video input queue length custom metric that is generated by the Go application running on the `video-queue-monitor` Compute Instance.
2. Add a chart for the high resolution video upload rate custom log based metric to the `Media_Dashboard` custom dashboard.

### Solution (Graphical User Interface): Monitoring/Dashboards

1. In the Cloud Console, click **Navigation menu** > **Monitoring** > **Dashboards**.
2. Click the custom dashboard named `Media_Dashboard`.
3. Click **VIEWING** on top right and then click **Switch to Editing mode** in the dropdown list.
4. Click **ADD CHART** and then click **Line**.
5. Add charts with the given resources and metrics.
   - The metric `input_queue_size` associated with the `gce_instance` resource type.
   - The metric `large_video_upload_rate`.

### Solution (Graphical User Interface): Monitoring/Metrics Explorer

1. In the Cloud Console, click **Navigation menu** > **Monitoring** > **Metrics Explorer**.
2. Find the given resource type and metric.
   - The metric `input_queue_size` associated with the `gce_instance` resource type.
   - The metric `large_video_upload_rate`.
3. Click **Save Chart**.
4. Keep the Chart Title field with default value and set the **Dashboard** as `Media_Dashboard`.
5. Click **SAVE**

### Reference

- [Cloud Monitoring: Qwik Start | Qwiklabs](https://google.qwiklabs.com/focuses/10599?parent=catalog)
- [Creating and managing dashboard widgets | Cloud Monitoring Documentation](https://cloud.google.com/monitoring/charts)

## Task 5: Create a Cloud Operations alert based on the rate of high resolution video file uploads

### Description

Create a custom alert using the high resolution video upload metric that triggers when the upload rate for large videos exceeds a count of 3 per minute.

### Solution (Graphical User Interface)

1. In the Cloud Console, click **Navigation menu** > **Monitoring** > **Alerting**.
2. Click **CREATE POLICY**.
3. Click **ADD CONDITION**
     - Find resource type `gae_instance` and metric `large_video_upload_rate`.
     - Setup the configuration with **Condition** `is above` for `3` minute.
4. Click **ADD** > **NEXT** > **NEXT**
5. Fill up the **Alert Name** (e.g. `High resolution video uploads`).
6. CLick **Save**

### Solution (Command Line Interface)

```bash
$ gcloud alpha monitoring policies create \
    --display-name="High resolution video uploads" \
    --condition-display-name="/logging/user/large_video_upload_rate [RATE]"\
    --condition-filter='metric.type="appengine.googleapis.com/flex/instance/cpu/utilization" resource.type="gae_instance"' \
    --duration="3m" \
    --if="> 5.0" \
    --combiner="AND"
```

### References

- [Cloud Monitoring: Qwik Start | Qwiklabs](https://google.qwiklabs.com/focuses/10599?parent=catalog)
- [Creating an alerting policy | Cloud Monitoring Documentation](https://cloud.google.com/monitoring/alerts/using-alerting-ui)
- [`gcloud alpha monitoring policies create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/alpha/monitoring/policies/create)
