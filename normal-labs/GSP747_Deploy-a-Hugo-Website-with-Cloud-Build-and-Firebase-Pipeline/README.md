# GSP747 —— Deploy a Hugo Website with Cloud Build and Firebase Pipeline

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Process Overview](#process-overview)
- [Benefits of Static Websites](#benefits-of-static-websites)
- [Deploy To Firebase](#deploy-to-firebase)
- [Cloud Build Trigger](#cloud-build-trigger)
- [References](#references)

</details>

## Overview

In this lab you will create a pipeline for deploying websites based on Hugo, a static website builder. You will store the website content in Cloud Source Repositories and deploy the website with Firebase, then use Cloud Build to create a pipeline to automatically deploy new content that is committed to the repository.

## Process Overview

<div align="center">
  <img src="https://i.imgur.com/HGyCg5O.png" alt="Process Overview">
</div>

The goal is to be able to commit code and have it trigger the pipeline which will in turn deploy the website. Your journey will be divided into tw o parts. First, you will build the website locally and deploy it to Firebase manually so you can gain an understanding of the entire process. Second, you will automate the process by building a pipeline with Cloud Build.

## Benefits of Static Websites

Static site builders like Hugo have become popular because of their ability to produce websites that do not require web servers. With static web platforms there are no server operating systems or software to maintain. There are, however, various operational considerations. For example, you may want to version control your postings, host your web site on a content delivery network ("CDN") and provision an SSL certificate.

You can address these needs by using a Continuous Integration / Continuous Deployment pipeline on Google Cloud. A deployment pipeline enables developers to rapidly innovate by automating the entire deployment process. In this lab, you will learn to build a pipeline that demonstrates this automation.

## Deploy To Firebase

```bash
# create repository and the initial web site
$ gcloud source repos create <REPO_NAME>
$ gcloud source repos clone <REPO_NAME>

# create and run the hugo site structure
$ hugo new site <SITE_NAME> --force
$ hugo server -D --bind <IP_ADDRESS> --port <PORT>

# deploy site to firebase
$ firebase init
$ hugo && firebase deploy
```

## Cloud Build Trigger

Building the pipeline to be able triggering builds when changes are made to the repository. The [Cloud Build](https://cloud.google.com/build) uses a file named [`cloudbuild.yaml`](https://cloud.google.com/build/docs/configuring-builds/create-basic-configuration) in the root directory of the repository to perform the build.

After creating the config file, follow the steps to create the Cloud Build trigger:

1. Click **Navigation Menu** > **Cloud Build** > **Triggers**.
2. Click **CREATE TRIGGER**.
3. Click **CREATE**.

Don't forget that the Cloud Build Service account needs to have permissions to use Firebase to deploy the website.

1. Click **Navigation Menu** > **IAM & Admin** > **IAM**.
2. Locate the entry containing `cloudbuild.gserviceaccount.com` and click the **Edit** button.
3. Click **ADD ANOTHER ROLE**.
4. Add the role **Firebase Products** > **Firebase Hosting Admin** to it.

## References

- [Hugo](https://gohugo.io/)
- [Cloud Build Documentation](https://cloud.google.com/build/docs)