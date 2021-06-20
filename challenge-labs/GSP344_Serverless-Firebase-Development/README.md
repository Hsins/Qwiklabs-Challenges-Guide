# GSP344 —— Serverless Firebase Development

<div align="center">
  <img src="https://i.imgur.com/XR1Xmjs.png" alt="GSP344 —— Serverless Firebase Development">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Challenge Scenario](#challenge-scenario)
- [Provision the Environment](#provision-the-environment)
- [Task 1: Create a Firestore database](#task-1-create-a-firestore-database)
  - [Description](#description)
  - [Solution](#solution)
- [Task 2: Populate the Database](#task-2-populate-the-database)
  - [Description](#description-1)
  - [Solution](#solution-1)
- [Task 3: Create a REST API](#task-3-create-a-rest-api)
  - [Description](#description-2)
  - [Solution](#solution-2)
- [Task 4: Firestore API access](#task-4-firestore-api-access)
  - [Description](#description-3)
  - [Solution](#solution-3)
- [Task 5: Deploy the Staging Frontend](#task-5-deploy-the-staging-frontend)
  - [Description](#description-4)
  - [Solution](#solution-4)
- [Task 6: Deploy the Production Frontend](#task-6-deploy-the-production-frontend)
  - [Description](#description-5)
  - [Solution](#solution-5)
- [References](#references)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| Fundamental | `GSP642` | [Importing Data to a Firestore Database](https://google.qwiklabs.com/focuses/8392?parent=catalog) | [EN](../../normal-labs/GSP642_Importing-Data-to-a-Firestore-Database/) |
| Fundamental | `GSP643` | [Build a Serverless Web App with Firebase](https://google.qwiklabs.com/focuses/8391?parent=catalog) | [EN](../../normal-labs/GSP643_Build-a-Serverless-Web-App-with-Firebase/) |
| Fundamental | `GSP747` | [Deploy a Hugo Website with Cloud Build and Firebase Pipeline](https://google.qwiklabs.com/focuses/14353?parent=catalog) | [EN](../../normal-labs/GSP747_Deploy-a-Hugo-Website-with-Cloud-Build-and-Firebase-Pipeline/) |
| Fundamental | `GSP174` | [Google Assistant: Build an Application with Dialogflow and Cloud Functions](https://google.qwiklabs.com/focuses/3634?parent=catalog) | [EN](../../normal-labs/GSP174_Google-Assistant-Build-an-Application-with-Dialogflow-and-Cloud-Functions/) |
| Advanced | `GSP344` | [Serverless Firebase Development: Challenge Lab](https://google.qwiklabs.com/focuses/14677?parent=catalog) |  |

</details>

## Overview

This lab is recommended for students who are enrolled in the [Serverless Firebase Development](https://google.qwiklabs.com/quests/153) quest.

Prerequisites:

- Firestore
- Cloud Run
- Cloud Build
- Container Registry

## Challenge Scenario

In this lab you will create a frontend solution using a Rest API and Firestore database. Cloud Firestore is a NoSQL document database that is part of the Firebase platform where you can store, sync, and query data for your mobile and web apps at scale. Lab content is based on resolving a real world scenario through the use of Google Cloud serverless infrastructure.

You will build the following architecture:

<div align="center">
  <img src="https://i.imgur.com/G0Qu42B.png" alt="Architecture">
</div>

## Provision the Environment

Link to the project:

```bash
$ gcloud config set project $(gcloud projects list --format='value(PROJECT_ID)' --filter='qwiklabs-gcp')
```

Clone the repo:

```bash
$ git clone https://github.com/rosera/pet-theory.git
```

## Task 1: Create a Firestore database

### Description

In this scenario you create a Firestore Database in Google Cloud. The high level architecture diagram below summarizes the general architecture.

<div align="center">
  <img src="https://i.imgur.com/pt1LfFU.png" alt="General Architecture">
</div>

Requirements:

| Field | Value |
| :--: | :-- |
| Cloud Firestore | Native Mode |
| Location | Nam5 (United States) |

To complete this section successfully, you are required to implement the following:

- Cloud Firestore Database
- Use Firestore Native Mode
- Add location Nam5 (United States)

### Solution

1. Click **Navigation Menu** > **Firestore**.
2. Click **SELECT NATIVE MODE**.
3. Select`nam5 (United States)` as the location.
4. Click **CREATE DATABASE**.

## Task 2: Populate the Database

### Description

In this scenario, populate the database using test data. A high level architecture diagram below summarizes the general architecture.

<div align="center">
  <img src="https://i.imgur.com/SpDAIAO.png" alt="General Architecture">
</div>

To complete this section successfully, you are required to implement the following tasks:

- Use the sample code from `pet-theory/lab06/firebase-import-csv/solution`.
- To import CSV use the node `pet-theory/lab06/firebase-import-csv/solution/index.js`.

### Solution

```bash
# navigate to target folder and install dependencies
$ cd ~/pet-theory/lab06/firebase-import-csv/solution
$ npm install

# import csv file
$ node index.js netflix_titles_original.csv
```

## Task 3: Create a REST API

### Description

In this scenario, create an example REST API. A high level architecture diagram below summarizes the general architecture.

<div align="center">
  <img src="https://i.imgur.com/atXA8AT.png" alt="General Architecture">
</div>

To complete this section successfully, you are required to implement the following tasks:

- Access `pet-theory/lab06/firebase-rest-api/solution-01`
- Build and Deploy the code to Google Container Registry
  - Container Registry Image:	`rest-api:0.1`
- Deploy the image as a Cloud Run Service
  - Cloud Run Service: `netflix-dataset-service`
  - Permission: `--allow-unauthenticated`
- `curl -X GET $SERVICE_URL` should respond with: `{"status":"Netflix Dataset! Make a query."}`

### Solution

```bash
# navigate to target folder and install dependencies
$ cd ~/pet-theory/lab06/firebase-rest-api/solution-01
$ npm install

# build and deploy the code to Google Container Registry (gcr)
$ gcloud builds submit --tag="gcr.io/$GOOGLE_CLOUD_PROJECT/rest-api:0.1"

# deploy the image as a Cloud Run Service
$ gcloud run deploy netflix-dataset-service \
    --region="us-central1" \
    --image="gcr.io/$GOOGLE_CLOUD_PROJECT/rest-api:0.1" \
    --allow-unauthenticated

# [Optional] check the resoponse
$ SERVICE_URL="<SERVICE_URL_OF_REST_API>"
$ curl -X GET $SERVICE_URL
```

## Task 4: Firestore API access

### Description

In this scenario, deploy an updated revision of the code to access the Firestore DB. A high level architecture diagram below summarizes the general architecture.

<div align="center">
  <img src="https://i.imgur.com/FSRW5bG.png" alt="General Architecture">
</div>

To complete this section successfully, you are required to implement the following tasks:

- Access `pet-theory/lab06/firebase-rest-api/solution-02`.
- Build the updated application
- Use Cloud Build to tag and deploy image revision to Container Registry
  - Container Registry Image:	`rest-api:0.2`
- Deploy the new image as Cloud Run service
  - Cloud Run Service: `netflix-dataset-service`
  - Permission: `--allow-unauthenticated`
- `curl -X GET $SERVICE_URL/2019` should respond with json dataset

### Solution

```bash
# navigate to target folder and install dependencies
$ cd ~/pet-theory/lab06/firebase-rest-api/solution-02
$ npm install

# build and deploy the code to Google Container Registry (gcr)
$ gcloud builds submit --tag="gcr.io/$GOOGLE_CLOUD_PROJECT/rest-api:0.2"

# deploy the image as a Cloud Run Service
$ gcloud run deploy netflix-dataset-service \
    --region="us-central1" \
    --image="gcr.io/$GOOGLE_CLOUD_PROJECT/rest-api:0.2" \
    --allow-unauthenticated

# [Optional] check the resoponse
$ SERVICE_URL="<SERVICE_URL_OF_NETFLIX_DATASET_SERVICE>"
$ curl -X GET $SERVICE_URL/2019
```

## Task 5: Deploy the Staging Frontend

### Description

In this scenario, deploy the Staging Frontend. A high level architecture diagram below summarizes the general architecture.

<div align="center">
  <img src="https://i.imgur.com/AOPkIls.png" alt="General Architecture">
</div>

To complete this section successfully, you are required to implement the following tasks:

- Access `pet-theory/lab06/firebase-frontend`
- Build the frontend staging application
- Use Cloud Build to tag and deploy image revision to Container Registry
  - Container Registry Image:	`frontend-staging:0.1`
- Deploy the new image as Cloud Run service
  - Cloud Run Service: `frontend-staging-service`
- Frontend access to Rest API and Firestore Database

### Solution

```bash
# edit the REST_API_SERVICE URL
$ cd ~/pet-theory/lab06/firebase-frontend/public
$ nano app.js

# navigate to target folder and install dependencies
$ cd ~/pet-theory/lab06/firebase-frontend
$ npm install

# build and deploy the code to Google Container Registry (gcr)
$ gcloud builds submit --tag="gcr.io/$GOOGLE_CLOUD_PROJECT/frontend-staging:0.1"

# deploy the image as a Cloud Run Service
$ gcloud run deploy frontend-staging-service \
    --region="us-central1" \
    --image="gcr.io/$GOOGLE_CLOUD_PROJECT/frontend-staging:0.1"
```

## Task 6: Deploy the Production Frontend

### Description

In this scenario, update the Staging Frontend to use the Firestore database. A high level architecture diagram below summarizes the general architecture.

<div align="center">
  <img src="https://i.imgur.com/ePEfSXn.png" alt="General Architecture">
</div>

To complete this section successfully, you are required to implement the following tasks:

- Access `pet-theory/lab06/firebase-frontend/public`
- Update the frontend application i.e. `app.js` to use the REST API
- Don't forget to append the year to the `SERVICE_URL`
- Use Cloud Build to tag and deploy image revision to Container Registry
  - Container Registry Image:	`frontend-production:0.1`
- Deploy the new image as Cloud Run service
  - Cloud Run Service: `frontend-production-service`
- Frontend access to Rest API and Firestore Database

### Solution

```bash
# navigate to target folder and install dependencies
$ cd ~/pet-theory/lab06/firebase-frontend
$ npm install

# build and deploy the code to Google Container Registry (gcr)
$ gcloud builds submit --tag="gcr.io/$GOOGLE_CLOUD_PROJECT/frontend-production:0.1"

# deploy the image as a Cloud Run Service
$ gcloud run deploy frontend-production-service \
    --region="us-central1" \
    --image="gcr.io/$GOOGLE_CLOUD_PROJECT/frontend-production:0.1"
```

## References

- [`gcloud builds submit` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/builds/submit)
- [`gcloud run deploy` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/run/deploy)