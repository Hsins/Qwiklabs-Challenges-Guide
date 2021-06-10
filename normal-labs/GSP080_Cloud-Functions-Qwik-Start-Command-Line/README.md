# GSP080 —— Cloud Functions: Qwik Start - Command Line

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

Cloud Functions can be written in Node.js, Python, and Go, and are executed in language-specific runtimes as well. You can take your Cloud Function and run it in any standard Node.js runtime which makes both portability and local testing a breeze.

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

```bash
$ gcloud functions deploy <FUNCTION-NAME> \
  --stage-bucket=<STAGE-BUCKET> \
  --trigger-topic=<TRIGGER-TOPIC> \
  --runtime=<RUNTIME>

# verify the status of the function
$ gcloud functions describe <FUNCTION-NAME>
```

## Test Functions and View Logs

```bash
# create test of the function
$ gcloud functions call <FUNCTION-NAME> --data <DATA>

# check the logs in the log history
$ gcloud functions logs read <FUNCTION-NAME>
```

## References

- [Connect & Extend GCP Services with Google Cloud Functions | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=_nYXeEe-hqc)
- [Cloud Functions Documentation](https://cloud.google.com/functions/docs)
- [Pub/Sub: A Google-Scale Messaging Service | Google Pub/Sub Documentation](https://cloud.google.com/pubsub/architecture)
- [Background Functions | Cloud Functions Documentation](https://cloud.google.com/functions/docs/writing/background)
- [Events and Triggers | Cloud Functions Documentation](https://cloud.google.com/functions/docs/concepts/events-triggers)
- [`gcloud functions deploy` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/functions/deploy)
- [`gcloud functions describe` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/functions/describe)
- [`gcloud functions call` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/functions/call)
- [`gcloud functions log` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/functions/log)