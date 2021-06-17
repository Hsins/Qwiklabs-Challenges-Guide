# GSP643 —— Build a Serverless Web App with Firebase

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Architecture](#architecture)
- [Enable the Google Cloud Firestore API](#enable-the-google-cloud-firestore-api)
- [Setup Firestore Database](#setup-firestore-database)
- [Create Firebase Project](#create-firebase-project)
- [Firebase CLI](#firebase-cli)
- [References](#references)

</details>

## Overview

For the labs in the [Google Cloud Run Serverless Workshop](https://google.qwiklabs.com/quests/98), you will read through a fictitious business scenario and assist the characters with their serverless migration plan.

Twelve years ago, Lily started the Pet Theory chain of veterinary clinics. The Pet Theory chain has expanded rapidly over the last few years. Their old appointment system is not able to handle the increased load or allow clients to schedule their own appointments, so Lily asked Patrick, in IT, and Ruby, a consultant, to build a cloud-based system that easily scale.

## Architecture

This diagram gives you an overview of the services you will be using and how they connect to one another:

<div align="center">
  <img src="https://i.imgur.com/1p84FHi.png" alt="Architecture">
</div>

## Enable the Google Cloud Firestore API

1. Click **Navigation Menu** > **APIs & Services** > **Library**.
2. Search for **"Firestore"**.
3. Click **Google Cloud Firestore API**.
4. Click **Enable**.

## Setup Firestore Database

1. Click **Navigation Menu** > **Firestore**.
2. Click **SELECT NATIVE MODE** or **SELECT DATASTORE MODE** button.
    - **Native Mode**: good for letting lots of users access the same data at the same time and it has features like real-time updates and direct connection between your database and web/mobile clients.
    - **Datastore Mode**: puts an emphasis on high throughput (lots of reads and writes).
3. Click **CREATE DATABASE**.

## Create Firebase Project

1. Open the [Firebase console](https://console.firebase.google.com/).
2. Click **Create Project**.
3. Select Project ID from drop-down menu and accept the Firebase terms.
4. Click **Continue**.
5. Click **Comfirm**.
6. Click **Continue**.
7. Click **Continue**.

## Firebase CLI

```bash
# install firebase cli
$ npm install -g firebase-tools

# login with firebase cli
$ firebase login --no-localhost

# deploy Firebase hosting
$ firebase init
$ firebase deploy
```

## References

- [Firestore Documentation](https://cloud.google.com/firestore/docs)
- [rosera/pet-theory | GitHub](https://github.com/rosera/pet-theory)
- [Firebase CLI reference | Firebase Documentation](https://firebase.google.com/docs/cli)