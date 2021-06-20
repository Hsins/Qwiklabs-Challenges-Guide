# GSP325 —— Build Interactive Apps with Google Assistant: Challenge Lab

<div align="center">
  <img src="https://i.imgur.com/lKaZmXN.png" alt="GSP324 —— Explore Machine Learning Models with Explainable AI">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Challenge Scenario](#challenge-scenario)
- [Your challenge](#your-challenge)
- [Task 1: Create the Cloud Function for the Magic Eight Ball app for Google Assistant](#task-1-create-the-cloud-function-for-the-magic-eight-ball-app-for-google-assistant)
  - [Description](#description)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface)
- [Task 2: Create the Lab Magic 8 Ball app for Google Assistant](#task-2-create-the-lab-magic-8-ball-app-for-google-assistant)
  - [Description](#description-1)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface-1)
- [Task 3: Add multilingual support to your `magic_eight_ball` Cloud Function](#task-3-add-multilingual-support-to-your-magic_eight_ball-cloud-function)
  - [Description](#description-2)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface-2)
- [References](#references)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| Introductory | `GSP263` | [Google Assistant: Qwik Start - Dialogflow](https://www.qwiklabs.com/focuses/2196?parent=catalog) | [EN](../../normal-labs/GSP263_Google-Assistant-Qwik-Start-Dialogflow/) |
| Introductory | `GSP294` | [Introduction to APIs in Google](https://google.qwiklabs.com/focuses/3473?parent=catalog) | [EN](../../normal-labs/GSP294_Introduction-to-APIs-in-Google/) |
| Fundamental | `GSP174` | [Google Assistant: Build an Application with Dialogflow and Cloud Functions](https://google.qwiklabs.com/focuses/3634?parent=catalog) | [EN](../../normal-labs/GSP174_Google-Assistant-Build-an-Application-with-Dialogflow-and-Cloud-Functions/) |
| Advanced | `GSP487` | [Google Assistant: Build a Youtube Entertainment App](https://google.qwiklabs.com/focuses/4785?parent=catalog) | [EN](../../normal-labs/GSP487_Google-Assistant-Build-a-YouTube-Entertainment-App/) |
| Advanced | `GSP486` | [Google Assistant: Build a Restaurant Locator with the Places API](https://google.qwiklabs.com/focuses/4784?parent=catalog) | [EN](../../normal-labs/GSP487_Google-Assistant-Build-a-YouTube-Entertainment-App/) |
| Expert | `GSP325` | [Build Interactive Apps with Google Assistant: Challenge Lab](https://google.qwiklabs.com/focuses/11881?parent=catalog) |  |

</details>

## Overview

This lab is recommended for students who have enrolled in the [Build Interactive Apps with Google Assistant](https://google.qwiklabs.com/quests/122?) quest.

Topics tested:

- Creating an Actions project
- Setup Dialogflow
- Configure Dialogflow intents
- Use a webhook in a Dialogflow intent
- Adding code to the right place to call the Google Translate API

## Challenge Scenario

As a junior developer in Jooli Inc. and recently trained with Google Cloud and Dialogflow you have been asked to help a new team (Taniwha) set up their environment. The team has asked for your help and has done some work, but needs you to complete the work.

You are expected to have the skills and knowledge for these tasks so don’t expect step-by-step guides.

## Your challenge

You need to help the team with some of their initial work creating two new Dialogflow apps.

As soon as you sit down at your desk and open your new laptop you receive the following request to complete these tasks. Good luck!

## Task 1: Create the Cloud Function for the Magic Eight Ball app for Google Assistant

### Description

Create a python Cloud Function that will produce the result. The code is below, make sure you set the **Entry point** name to `magic_eight_ball`. Make sure you grant **Cloud Functions Invoker** to `allUsers`.
**Cloud Functions Invoker**

<details>
  <summary>
    <strong><code>main.py</code></strong>
  </summary>

  ```python
  import random
  import logging
  import google.cloud.logging
  from google.cloud import translate_v2 as translate
  from flask import Flask, request, make_response, jsonify

  def magic_eight_ball(request):

      client = google.cloud.logging.Client()
      client.get_default_handler()
      client.setup_logging()

      choices = [
          "It is certain.", "It is decidedly so.", "Without a doubt.",
          "Yes - definitely.", "You may rely on it.", "As I see it, yes.",
          "Most likely.", "Outlook good.", "Yes.","Signs point to yes.",
          "Reply hazy, try again.", "Ask again later.",
          "Better not tell you now.", "Cannot predict now.",
          "Concentrate and ask again.", "Don't count on it.",
          "My reply is no.", "My sources say no.", "Outlook not so good.",
          "Very doubtful."
      ]

      magic_eight_ball_response = random.choice(choices)

      logging.info(magic_eight_ball_response)

      return make_response(jsonify({'fulfillmentText': magic_eight_ball_response }))
  ```

</details>

<details>
  <summary>
    <strong><code>requirements.txt</code></strong>
  </summary>

  ```
  google-cloud-translate
  google-cloud-logging
  ```

</details>

### Solution (Graphical User Interface)

1. Click **Navigation Menu** > **Cloud Functions**.
2. Click **CREATE FUNCTION**.
    - **Name**: `magic_eight_ball`
3. Click **Save** > **Next**
    - **Entry Point**: `magic_eight_ball`
    - **Runtime**: `Python 3.7`
4. Click **DEPLOY**

## Task 2: Create the Lab Magic 8 Ball app for Google Assistant

### Description

Use the [Actions Console](https://console.actions.google.com/) to start to creating an action that has the following flow:

- **App**: Welcome to the lab magic 8 ball, ask me a yes or no question and I will predict the future!
- **User**: Will I complete this challenge lab?
- **App**: Cannot predict now.

You need to configure:

- a fulfillment that enables a webhook to your cloud function created in task 1.
- the **Default Welcome Intent Text Response** to `Welcome to the lab magic 8 ball, ask me a yes or no question and I will predict the future!`
- the **Default Fallback Intent** to enable **Set this intent as end of conversation** and enable **Enable webhook call for this intent**

### Solution (Graphical User Interface)

First, we're going to create the Action Project.

1. Go to [Actions Console](https://console.actions.google.com/).
2. Click **Build Your Action**.
    - **Display Name**: `<INITIAL> magic 8 ball`.
3. Click **Save**.

Let's build the Actions in the project.

1. Click **Actions** > **Get Started** > **Custom Intent** > **BUILD**.
3. Accept the agreements and click **Accept**.
4. Click **CREATE** in the Dialogflow agent creation page.

After buliding the Actions, we're going to setup the action.

- Setup **Fulfillment**.
   1. Click **Fulfillment** from the left-hand menu.
   2. Move the silder for **Webhook** to **ENABLED**
   3. **URL**: `<CLOUD_FUNCTION_URL>` (Copy from Task 1)
- Setup **Default Welcome Intent Text Response**
   1. Click **Intents** from the left-hand menu.
   2. Click **Default Welcome Intent**.
   3. Move to the **Response** section and delete all text responses.
   4. Click **Add Response** > **Text Response**.
   5. Add `Welcome to the lab magic 8 ball, ask me a yes or no question and I will predict the future!`
   6. Click **Save**
- Setup **Default Fallback Intent**
   1. Click **Intents** from the left-hand menu.
   2. Click **Default Fallback Intent**.
   3. Enable **Set this intent as end of conversation**.
   4. Move to the **Fulfillment** section and click **Enable fulfillment**.
   5. Move the silder for **Enable webhook call for this intent** to the right.
   6. Click **Save**

Now we can test the Assistant application.

1. Click **Integration** from the left-hand menu.
2. Click **Integration Settings** > **TEST**.
3. Enter `Will I complete this challenge lab?`.

## Task 3: Add multilingual support to your `magic_eight_ball` Cloud Function

### Description

Add the following code to your `magic_eight_ball` cloud function. You need to determine where to insert the code.

```python
    request_json = request.get_json()

    if request_json and 'queryResult' in request_json:
        question = request_json.get('queryResult').get('queryText')

    # try to identify the language
    language = 'en'
    translate_client = translate.Client()
    detected_language = translate_client.detect_language(question)
    if detected_language['language'] == 'und':
        language = 'en'
    elif detected_language['language'] != 'en':
        language = detected_language['language']

    # translate if not english
    if language != 'en':
        logging.info('translating from en to %s' % language)
        translated_text = translate_client.translate(
             magic_eight_ball_response, target_language=language)
        magic_eight_ball_response = translated_text['translatedText']
```

Test with the following sentences in non-English languages:

- `我会完成这个挑战实验室吗？`
- `¿Completaré este laboratorio de desafío?`
- `இந்த சவால் ஆய்வகத்தை நான் முடிக்கலாமா?`

### Solution (Graphical User Interface)

First, update the Cloud Function code to add multilingual support.

1. Go to [**Cloud Console**](https://console.cloud.google.com/).
2. Click **Navigation Menu** > **Cloud Functions**.
3. Click the cloud function **magic_eight_ball** create in Task 1.
4. Click **Edit** > **Next**
    - Insert the given Python code after `magic_eight_ball_response = random.choice(choices)` (line 18).
5. Click **DEPLOY**

After the status of deployment is OK, test the Assistant application with sentences in non-English languages:

1. Go back to the Dialogflow Page.
2. Click **Integration** from the left-hand menu.
3. Click **Integration Settings** > **TEST**.
4. Test with following sentences:
    - `我会完成这个挑战实验室吗？`
    - `¿Completaré este laboratorio de desafío?`
    - `இந்த சவால் ஆய்வகத்தை நான் முடிக்கலாமா?`

## References

- [Google Assistant Documentation](https://developers.google.com/assistant)