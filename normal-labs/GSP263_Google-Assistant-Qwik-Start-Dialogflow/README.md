# GSP263 —— Google Assistant: Qwik Start - Dialogflow

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Create Actions Project](#create-actions-project)
- [Setup Dialogflow](#setup-dialogflow)
- [Build Custom Dialogflow Intents](#build-custom-dialogflow-intents)
- [References](#references)

</details>

## Overview

[Google Assistant](https://assistant.google.com/#?modal_active=none) is a personal voice assistant that offers a host of actions and integrations. From sending texts and setting reminders, to ordering coffee and playing your favorite songs, the 1 million+ actions available suit a wide range of voice command needs. Google Assistant is offered on Android and iOS, but it can even be integrated with other devices like smartwatches, Google Homes, and Android TVs.

As you will soon find out, [Actions](https://developers.google.com/assistant) is the central platform for developing Google Assistant applications. Actions work with a number of human-computer interaction suites, which simplifies conversational app development. Out of all the platforms, the most popular is [Dialogflow](https://dialogflow.com/), which uses an underlying machine learning (ML) and natural language understanding (NLU) schema to build rich Assistant applications.

## Create Actions Project

Before we start building our quotation generator, let's review the following terms:

- **Google Assistant** is the virtual assistant that's found on smartphones, homes, and a host of other devices. It's the application that takes in voice commands and completes tasks based on user input.
- **Actions on Google** is the developer platform that allows you to build applications for Google Assistant. This is going to be the central console for conversational application development.

Let's build the Actions Project.

1. Open [Actions Console](http://console.actions.google.com/).
2. Click **New Project** and agree the Terms of Service.
3. Select **Project ID** and click **IMPORT PROJECT**.

## Setup Dialogflow

Dialogflow is a platform that abstracts the complexities of NLU and ML to build conversational applications. Follow the step to setup Dialogflow:

1. Go to **Build your Action** > **Add Action(s)**.
2. Click **Get started**.
3. Select **Custom Intent** > **BUILD**.
4. Click **CREATE** in the top right corner in the Dialogflow agent page.

In Dialogflow, there're some terms should be known:

- **Action**: an interaction built for Google Assistant that performs specific tasks based on user input.
- **Intent**: the goal of the Action (e.g. generate quotes). An intent takes user input and channels it to trigger an event.
- **Agent (Dialogflow)**: a module that uses NLU and ML to transform user input into actionable data to be used by an Assistant application.

## References

- [Actions on Google glosssary | Google Assistant Documentation](https://developers.google.com/assistant/conversational/df-asdk/glossary)
- [Actions](https://developers.google.com/assistant)
- [Dialogflow](https://dialogflow.com/)
