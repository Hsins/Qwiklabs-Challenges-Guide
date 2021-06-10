# GSP081 —— Cloud Functions: Qwik Start - Console

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Cloud Functions](#cloud-functions)
- [Create and Deploy Functions](#create-and-deploy-functions)
- [Test Functions and View Logs](#test-functions-and-view-logs)
- [References](#references)

</details>

## Overview

Cloud Functions is a serverless execution environment for building and connecting cloud services. With Cloud Functions you write simple, single-purpose functions that are attached to events emitted from your cloud infrastructure and services. Your Cloud Function is triggered when an event being watched is fired. Your code executes in a fully managed environment. There is no need to provision any infrastructure or worry about managing any servers.

Cloud Functions are written in Javascript and execute in a Node.js environment on Google Cloud. You can take your Cloud Function and run it in any standard Node.js runtime which makes both portability and local testing a breeze.

## Cloud Functions

- Cloud Functions is a serverless execution environment for building and connecting cloud services.
- The code executes in a fully managed environment and it's no need to provision any infrastructure.
- Cloud Functions triggered by the Cloud Events (things that happen in the cloud environment).
  - e.g. changes to data in a database
  - e.g. files added to a storage system
  - e.g. a new virtual machine instance being created
- Use Cases
  - e.g. Data Processing / ETL
  - e.g. Webhooks
  - e.g. Lightweight APIs
  - e.g. Mobile Backend
  - e.g. IoT

## Create and Deploy Functions

1. In the console, click the **Navigation Menu** > **Cloud Functions**.
2. Click **CREATE FUNCTION**.
3. In the **Create Function** dialog, fill up the fields.
4. Click **DEPLOY**.

After you click **DEPLOY**, the console redirects to the **Cloud Functions Overview** page. While the function is being deployed, the icon next to it is a small spinner. When it's deployed, the spinner is a green check mark.

## Test Functions and View Logs

- [Test Functions] In the **Cloud Functions Overview** page, display the menu for your function, and click **Test function**.
- [View Logs] In the **Cloud Functions Overview** page, display the menu for your function, and click **View logs**.

## References

- [Connect & Extend GCP Services with Google Cloud Functions | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=_nYXeEe-hqc)
- [Cloud Functions Documentation](https://cloud.google.com/functions/docs)
- [Events and Triggers | Cloud Functions Documentation](https://cloud.google.com/functions/docs/concepts/events-triggers)