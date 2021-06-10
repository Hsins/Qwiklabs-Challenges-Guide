# GSP096 —— Google Cloud Pub/Sub: Qwik Start - Console

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Setup Pub/Sub](#setup-pubsub)
    - [Create Topics](#create-topics)
    - [Add Subscriptions](#add-subscriptions)
- [Publish and View Messages](#publish-and-view-messages)
  - [Publish Messages](#publish-messages)
  - [View Messages](#view-messages)
- [References](#references)

</details>

## Overview

Google Cloud Pub/Sub is a messaging service for exchanging event data among applications and services. A producer of data publishes messages to a Cloud Pub/Sub topic. A consumer creates a subscription to that topic. Subscribers either pull messages from a subscription or are configured as webhooks for push subscriptions. Every subscriber must acknowledge each message within a configurable window of time.

## Setup Pub/Sub

To use a Pub/Sub, we have to create a topic to hold data and a subscription to access data published to the topic.

- A publisher application creates and sends messages to a **topic**.
- Subscriber applications create a **subscription** to a topic to receive messages from it.
- Cloud Pub/Sub is an asynchronous messaging service designed to be highly reliable and scalable.

#### Create Topics

1. Click **Navigation Menu** > **Pub/Sub** > **Topics**.
2. Click **CREATE TOPIC**.
3. Fill up fields in the **Create a topic** dialog.
4. Click **CREATE TOPIC**

#### Add Subscriptions

1. Click **Navigation Menu** > **Pub/Sub** > **Topics**.
2. For the topics we've made, click the **three dot icon** > **Create subscription**.
3. Fill up fields in the **Add subscription to topic** dialog
4. Click **CREATE**

## Publish and View Messages

### Publish Messages

1. At the top of the **Topics details** dialog, click **PUBLISH MESSAGE**.
2. Enter messages in the Message field and click **PUBLISH**.

### View Messages

To view the message, we're going to use the subscription to pull the messages from the topic. Enter the following command in command line.

```bash
$ gcloud pubsub subscriptions pull --auto-ack <SUBSCRIPTION_NAME>
```

The message appears in the DATA field of the command output.

## References

- [Simplify Event Driven Processing with Cloud Pub/Sub | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=oKU2wbTXMTY)
- [Pub/Sub documentation](https://cloud.google.com/pubsub/docs)
