# GSP174 —— Google Assistant: Build an Application with Dialogflow and Cloud Functions

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Create Actions Project](#create-actions-project)
- [Build Action](#build-action)
- [Configure Cloud Function](#configure-cloud-function)
- [References](#references)

</details>

## Overview

[Google Assistant](https://assistant.google.com/) is a personal voice assistant that offers a host of actions and integrations. From making appointments and setting reminders, to ordering coffee and playing music, the 1 million+ actions available suit a wide range of voice command tasks. Google Assistant is offered on Android and iOS, but it can even be integrated with other devices like smartwatches, Google Homes, and Android TVs.

[Actions](https://developers.google.com/assistant) is the central platform for developing Google Assistant applications. The Actions platform integrates with human-computer interaction suites, which simplifies conversational app development. The most widely used suite is [Dialogflow](https://dialogflow.com/), which uses an underlying machine learning (ML) and natural language understanding (NLU) schema to build rich Assistant applications. The Actions platform also integrates with [Cloud Functions](https://cloud.google.com/functions/), which lets you run backend fulfillment code in response to events triggered by Dialogflow requests.

## Create Actions Project

1. Open [Actions Console](http://console.actions.google.com/) and sign in.
2. Click **New Project**.
3. Click **IMPORT PROJECT**.

## Build Action

An [action](https://developers.google.com/assistant/conversational/df-asdk/glossary#A) is an interaction you build for the Google Assistant. An action supports a specific [intent](https://developers.google.com/actions/glossary#intent) (a goal or task that users want to accomplish), which is carried out by a corresponding [fulfillment](https://developers.google.com/assistant/conversational/df-asdk/glossary#fulfillment) (logic that handles an intent and carries out the corresponding Action).

1. Click on the Project Name.
2. Click **Build Your Action** > **Add Action(s)** > **Get Started**.
3. Select **Custom Intent** > **BUILD**.
4. Click **CREATE**.

An [agent](https://dialogflow.com/docs/agents) is an organizational unit that collects information needed to complete a user's request, which it then forwards to a service that provides fulfillment logic.

## Configure Cloud Function

1. Click **Navigation Menu** > **Cloud Functions**.
2. Click **CREATE FUNCTION**.

## References

- [Google Assistant](https://assistant.google.com/)
- [Actions](https://developers.google.com/assistant)
- [Dialogflow](https://dialogflow.com/)
- [Cloud Functions](https://cloud.google.com/functions/)
- [Conversational Actions Documentation](https://developers.google.com/actions/discovery/)