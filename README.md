<!-- Badge for License -->
<div align="right">

  [![](https://img.shields.io/github/license/Hsins/Qwiklabs-Challenges-Guide.svg?style=flat-square)](./LICENSE)

</div>

<!-- Logo, Title and Description -->
<div align="center">

  <img src="https://i.imgur.com/e9DkzyW.png" alt="Qwiklabs Challenges Guide" height="150px">

# Qwiklabs Challenges Guide

📘 _Guideline note on the challenge labs in the great online Google Cloud Platform (GCP) self-paced learning platform [Qwiklabs](https://www.qwiklabs.com/)_

[![](https://img.shields.io/badge/Qwikilabs%20Profile-H.H.%20Peng-f5cd0e?logo=qwiklabs&style=for-the-badge)](https://google.qwiklabs.com/public_profiles/2c8fea0b-b474-4c11-80fe-223c635be395)
[![](https://img.shields.io/badge/Skill%20Badges-5/26-54b848?logo=data:image/svg%2bxml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pg0KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDE5LjAuMCwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPg0KPHN2ZyB2ZXJzaW9uPSIxLjEiIGlkPSJMYXllcl8xIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB4PSIwcHgiIHk9IjBweCINCgkgdmlld0JveD0iMCAwIDQ2MCA0NjAiIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDQ2MCA0NjA7IiB4bWw6c3BhY2U9InByZXNlcnZlIj4NCjxnPg0KCTxwYXRoIHN0eWxlPSJmaWxsOiM3MUUyRjA7IiBkPSJNMjMwLDBDMTAyLjk3NSwwLDAsMTAyLjk3NCwwLDIzMGMwLDk4LjE4LDYxLjUxNywxODEuOTkzLDE0OC4xMDksMjE0Ljk5NGwzMDguODEzLTI1Mi43MDkNCgkJQzQzOC45MjgsODMuMjAyLDM0NC4xODEsMCwyMzAsMHoiLz4NCgk8cGF0aCBzdHlsZT0iZmlsbDojMzhDNkQ5OyIgZD0iTTQ1Ni45MDUsMTkyLjI4OEwzNDAuMzA3LDc1LjY5TDc0LDM3MC44NjVsNzQuMTEyLDc0LjExMkMxNzMuNTU0LDQ1NC42NzQsMjAxLjE1Myw0NjAsMjMwLDQ2MA0KCQljMTI3LjAyNSwwLDIzMC0xMDIuOTc1LDIzMC0yMzBDNDYwLDIxNy4xNTQsNDU4LjkyOSwyMDQuNTYsNDU2LjkwNSwxOTIuMjg4eiIvPg0KCTxwb2x5Z29uIHN0eWxlPSJmaWxsOiM1NDg4QTg7IiBwb2ludHM9IjE0Mi4wNzQsMjE5Ljk4MSA3NCwzNzAuODY1IDE0MC43ODMsMzY4LjEwMyAxODIuOTA3LDQyMCAyNTAuOTgxLDI2OS4xMTYgCSIvPg0KCTxwb2x5Z29uIHN0eWxlPSJmaWxsOiMyNzNCN0E7IiBwb2ludHM9IjMxNy45MjYsMjE5Ljk4MSAzODYsMzcwLjg2NSAzMTkuMjE3LDM2OC4xMDMgMjc3LjA5Myw0MjAgMjA5LjAxOSwyNjkuMTE2IAkiLz4NCgk8cGF0aCBzdHlsZT0iZmlsbDojRDQ4QjA3OyIgZD0iTTM4NiwxODZjMCw4Ni4xNTYtNjkuODQ0LDE1Ni0xNTYsMTU2TDExOS45MDgsMTg2TDIzMCwzMEMzMTYuMTU2LDMwLDM4Niw5OS44NDQsMzg2LDE4NnoiLz4NCgk8cGF0aCBzdHlsZT0iZmlsbDojRkZDNjFCOyIgZD0iTTc0LDE4NmMwLDg2LjE1Niw2OS44NDQsMTU2LDE1NiwxNTZWMzBDMTQzLjg0NCwzMCw3NCw5OS44NDQsNzQsMTg2eiIvPg0KCTxwYXRoIHN0eWxlPSJmaWxsOiNGRkZGRkY7IiBkPSJNMzQ1LjkyLDE4NS45OTVMMjMwLDgwLjA3NWMtMTAwLDE0LTExNS45MiwxMDUuOTItMTE1LjkyLDEwNS45Mg0KCQljLTAuMDA1LDYzLjkyNiw1MS45OTksMTE1LjkzLDExNS45MiwxMTUuOTNDMjkzLjkxMywzMDEuOTI1LDM0NS45MDksMjQ5LjkzNSwzNDUuOTIsMTg1Ljk5NXoiLz4NCgk8cGF0aCBzdHlsZT0iZmlsbDojRkVFMTg3OyIgZD0iTTEzNC4wOCwxODUuOTk1YzAtNTIuODksNDMuMDMtOTUuOTIsOTUuOTItOTUuOTJ2MTkxLjg1YzUyLjg5LDAsOTUuOTItNDMuMDMsOTUuOTItOTUuOTNoMjANCgkJYzAuMDA1LTYzLjkxNy01MS45OTktMTE1LjkyLTExNS45Mi0xMTUuOTJjLTYzLjkxNiwwLTExNS45MTMsNTEuOTkzLTExNS45MiwxMTUuOTA4QzExNC4wOCwxODUuOTk1LDEzNC4wOCwxODUuOTk1LDEzNC4wOCwxODUuOTk1DQoJCXoiLz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjxnPg0KPC9nPg0KPGc+DQo8L2c+DQo8Zz4NCjwvZz4NCjwvc3ZnPg0K&style=for-the-badge)](https://google.qwiklabs.com/catalog?keywords=skill_badge&format%5B%5D=quests)

</div>

- Thanks the [Cloud Study Jam 2021 (Taiwan/Hong Kong)](https://events.withgoogle.com/cloud-study-jam-2021-twhk/) event for offering 30-days free Qwiklabs subscription.

## Challenge Labs

| Level | Skill Badges Quest | Code | Note | Solution |
| :--: | :-- | :--: | :--: | :--: |
| Advanced | [Cloud Architecture: Design, Implement, and Manage](https://google.qwiklabs.com/quests/124) | [`GSP101`](https://www.qwiklabs.com/focuses/1734?parent=catalog) |  |  |
| Advanced | [Automate Interactions with Contact Center AI](https://google.qwiklabs.com/quests/127) | [`GSP311`](https://www.qwiklabs.com/focuses/12008?parent=catalog) |  |  |
| Introductory | [Create and Manage Cloud Resources](https://google.qwiklabs.com/quests/120) | [`GSP313`](https://www.qwiklabs.com/focuses/10258?parent=catalog) | [EN](./challenge-labs/GSP313_Create-and-Manage-Cloud-Resources/) |  |
| Expert | [Deploy and Manage Cloud Environments with Google Cloud](https://google.qwiklabs.com/quests/120) | [`GSP314`](https://www.qwiklabs.com/focuses/10417?parent=catalog) |  |  |
| Introductory | [Perform Foundational Infrastructure Tasks in Google Cloud](https://google.qwiklabs.com/quests/118) | [`GSP315`](https://www.qwiklabs.com/focuses/10379?parent=catalog) | [EN](./challenge-labs/GSP315_Perform-Foundational-Infrastructure-Tasks-in-Google-Cloud/) |  |
| Advanced | [Deploy to Kubernetes in Google Cloud](https://google.qwiklabs.com/quests/116) | [`GSP318`](https://www.qwiklabs.com/focuses/10457?parent=catalog) |  |  |
| Fundamental | [Build a Website on Google Cloud](https://google.qwiklabs.com/quests/115) | [`GSP319`](https://www.qwiklabs.com/focuses/11765?parent=catalog) |  |  |
| Advanced | [Set Up and Configure a Cloud Environment in Google Cloud](https://google.qwiklabs.com/quests/119) | [`GSP321`](https://www.qwiklabs.com/focuses/10603?parent=catalog) |  |  |
| Advanced | [Build and Secure Networks in Google Cloud](https://www.qwiklabs.com/quests/128) | [`GSP322`](https://google.qwiklabs.com/focuses/12068?parent=catalog) |  |  |
| Introductory | [Perform Foundational Data, ML, and AI Tasks in Google Cloud](https://www.qwiklabs.com/quests/117) | [`GSP323`](https://google.qwiklabs.com/focuses/11044?parent=catalog) |  |  |
| Fundamental | [Explore Machine Learning Models with Explainable AI](https://www.qwiklabs.com/quests/126) | [`GSP324`](https://google.qwiklabs.com/focuses/12011?parent=catalog) | [EN](./challenge-labs/GSP324_Explore-Machine-Learning-Models-with-Explainable-AI/) |  |
| Fundamental | [Build Interactive Apps with Google Assistant](https://www.qwiklabs.com/quests/122) | [`GSP325`](https://google.qwiklabs.com/focuses/11881?parent=catalog) |  |  |
| Advanced | [Engineer Data in Google Cloud](https://google.qwiklabs.com/quests/132) | [`GSP327`](https://www.qwiklabs.com/focuses/12379?parent=catalog) |  |  |
| Advanced | [Serverless Cloud Run Development](https://www.qwiklabs.com/quests/152) | [`GSP328`](https://google.qwiklabs.com/focuses/14744?parent=catalog) |  |  |
| Advanced | [Integrate with Machine Learning APIs](https://www.qwiklabs.com/quests/136) | [`GSP329`](https://google.qwiklabs.com/focuses/12704?parent=catalog) |  |  |
| Introductory | [Implement DevOps in Google Cloud](https://google.qwiklabs.com/quests/141) | [`GSP330`](https://www.qwiklabs.com/focuses/13287?parent=catalog) |  |  |
| Advanced | [Secure Workloads in Google Kubernetes Engine](https://google.qwiklabs.com/quests/142) | [`GSP335`](https://www.qwiklabs.com/focuses/13389?parent=catalog) |  |  |
| Fundamental | [Monitor and Log with Google Cloud Operations Suite](https://www.qwiklabs.com/quests/143) | [`GSP338`](https://www.qwiklabs.com/focuses/13786?parent=catalog) | [EN](./challenge-labs/GSP338_Monitor-and-Log-with-Google-Cloud-Operations-Suite/) |  |
| Introductory | Build and Optimize Data Warehouses with BigQuery | [`GSP340`](https://www.qwiklabs.com/focuses/14341?parent=catalog) |  |  |
| Fundamental | [Create ML Models with BigQuery ML](https://google.qwiklabs.com/quests/146) | [`GSP341`](https://google.qwiklabs.com/focuses/14294?parent=catalog) |  |  |
| Fundamental | [Ensure Access & Identity in Google Cloud](https://www.qwiklabs.com/quests/150) | [`GSP342`](https://www.qwiklabs.com/focuses/14572?parent=catalog) | [EN](./challenge-labs/GSP342_Ensure-Access-and-Identity-in-Google-Cloud/) |  |
| Advanced | [Optimize Costs for Google Kubernetes Engine](https://google.qwiklabs.com/quests/157) | [`GSP343`](https://www.qwiklabs.com/focuses/16327?parent=catalog) |  |  |
| Fundamental | [Serverless Firebase Development](https://google.qwiklabs.com/quests/153) | [`GSP344`](https://www.qwiklabs.com/focuses/14677?parent=catalog) |  |  |
| Introductory | Automating Infrastructure on Google Cloud with Terraform | [`GSP345`](https://www.qwiklabs.com/focuses/16502?parent=catalog) |  |  |
| Introductory | [Exploring Data with Looker](https://google.qwiklabs.com/quests/165) | [`GSP346`](https://www.qwiklabs.com/focuses/18116?parent=catalog) |  |  |
| Introductory | [Insights from Data with BigQuery](https://google.qwiklabs.com/quests/123) | [`GSP787`](https://www.qwiklabs.com/focuses/11988?parent=catalog) | [EN](./challenge-labs/GSP787_Insights-from-Data-with-BigQuery/) |  |

## Normal Labs

| Level | Code | Lab Name | Note |
| :--: | :--: | :-- | :--: |
| Introductory | `GSP001` | [Creating a Virtual Machine](https://google.qwiklabs.com/focuses/3563?parent=catalog) | [EN](../../normal-labs/GSP001_Creating-a-Virtual-Machine/) |
| Introductory | `GSP002` | [Getting Started with Cloud Shell and gcloud](https://google.qwiklabs.com/focuses/563?parent=catalog) | [EN](../../WorkSpace/Qwiklabs-Challenges-Guide/normal-labs/GSP002_Getting-Started-with-Cloud-Shell-and-gcloud/) |
| Fundamental | `GSP007` | [Set Up Network and HTTP Load Balancers](https://google.qwiklabs.com/focuses/12007?parent=catalog) | [EN](./normal-labs/GSP007_Set-Up-Network-and-HTTP-Load-Balancers/) |
| Introductory | `GSP055` | [Introduction to Docker](https://google.qwiklabs.com/focuses/1029?parent=catalog) | [EN](./normal-labs/GSP055_Introduction-to-Docker/) |
| Introductory | `GSP064` | [Cloud IAM: Qwik Start](https://google.qwiklabs.com/focuses/551?parent=catalog) | [EN](./normal-labs/GSP064_Cloud-IAM-Qwik-Start/) |
| Introductory | `GSP071` | [BigQuery: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/577?parent=catalog) | [EN](./normal-labs/GSP071_BigQuery-Qwik-Start-Command-Line/) |
| Introductory | `GSP072` | [BigQuery: Qwik Start - Console](https://google.qwiklabs.com/focuses/1145?parent=catalog) | [EN](./normal-labs/GSP072_BigQuery-Qwik-Start-Console/) |
| Introductory | `GSP073` | [Cloud Storage: Qwik Start - Cloud Console](https://google.qwiklabs.com/focuses/1760?parent=catalog) | [EN](./normal-labs/GSP073_Cloud-Storage-Qwik-Start-Cloud-Console/) |
| Introductory | `GSP074` | [Cloud Storage: Qwik Start - CLI/SDK](https://google.qwiklabs.com/focuses/569?parent=catalog) | [EN](./normal-labs/GSP074_Cloud-Storage-Qwik-Start-CLI-SDK/) |
| Introductory | `GSP076` | [AI Platform: Qwik Start](https://www.qwiklabs.com/focuses/581?parent=catalog) | [EN](./normal-labs/GSP076_AI-Platform-Qwik-Start/) |
| Introductory | `GSP080` | [Cloud Functions: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/916?parent=catalog) | [EN](./normal-labs/GSP080_Cloud-Functions-Qwik-Start-Command-Line/) |
| Introductory | `GSP081` | [Cloud Functions: Qwik Start - Console](https://google.qwiklabs.com/focuses/1763?parent=catalog) | [EN](./normal-labs/GSP081_Cloud-Functions-Qwik-Start-Console/) |
| Advanced | `GSP087` | [Autoscaling an Instance Group with Custom Cloud Monitoring Metrics](https://google.qwiklabs.com/focuses/611?parent=catalog) | [EN](./normal-labs/GSP087_Autoscaling-an-Instance-Group-with-Custom-Cloud-Monitoring-Metrics/)|
| Introductory | `GSP089` | [Cloud Monitoring: Qwik Start](https://google.qwiklabs.com/focuses/10599?parent=catalog) | [EN](./normal-labs/GSP089_Cloud-Monitoring-Qwik-Start/) |
| Fundamental | `GSP090` | [Monitoring Multiple Projects with Cloud Monitoring](https://google.qwiklabs.com/focuses/10621?parent=catalog) | [EN](./normal-labs/GSP090_Monitoring-Multiple-Projects-with-Cloud-Monitoring/) |
| Advanced | `GSP091` | [Creating and Alerting on Logs-based Metrics](https://google.qwiklabs.com/focuses/619?parent=catalog) | [EN](./normal-labs/GSP091_Creating-and-Alerting-on-Logs-based-Metrics/) |
| Fundamental | `GSP092` | [Monitoring and Logging for Cloud Functions](https://google.qwiklabs.com/focuses/1833?parent=catalog) | [EN](./normal-labs/GSP092_Monitoring-and-Logging-for-Cloud-Functions/) |
| Introductory | `GSP093` | [Compute Engine: Qwik Start - Windows](https://google.qwiklabs.com/focuses/560?parent=catalog) | [EN](./Qwiklabs-Challenges-Guide/normal-labs/GSP093_Compute-Engine-Qwik-Start-Windows/) |
| Introductory | `GSP094` | [Google Cloud Pub/Sub: Qwik Start - Python](https://google.qwiklabs.com/focuses/2775?parent=catalog) | [EN](./Qwiklabs-Challenges-Guide/normal-labs/GSP094_Google-Cloud-Pub-Sub-Qwik-Start-Python/) |
| Introductory | `GSP095` | [Google Cloud Pub/Sub: Qwik Start - Command Line](https://google.qwiklabs.com/focuses/925?parent=catalog) | [EN](./normal-labs/GSP095_Google-Cloud-Pub-Sub-Qwik-Start-Command-Line/) |
| Introductory | `GSP096` | [Google Cloud Pub/Sub: Qwik Start - Console](https://google.qwiklabs.com/focuses/3719?parent=catalog) | [EN](./normal-labs/GSP096_Google-Cloud-Pub-Sub-Qwik-Start-Console%20copy%202/) |
| Introductory | `GSP100` | [Kubernetes Engine: Qwik Start](https://google.qwiklabs.com/focuses/878?parent=catalog) | [EN](./normal-labs/GSP100_Kubernetes-Engine-Qwik-Start/) |
| Fundamental | `GSP111` | [Reporting Application Metrics into Cloud Monitoring](https://google.qwiklabs.com/focuses/1259?parent=catalog) | [EN](./normal-labs/GSP111_Reporting-Application-Metrics-into-Cloud-Monitoring/) |
| Introductory | `GSP190` | [IAM Custom Roles](https://google.qwiklabs.com/focuses/1035?parent=catalog) | [EN](./normal-labs/GSP190_IAM-Custom-Roles/) |
| Introductory | `GSP281` | [Introduction to SQL for BigQuery and Cloud SQL](https://google.qwiklabs.com/focuses/2802?parent=catalog) | [EN](./normal-labs/GSP281_Introduction-to-SQL-for-BigQuery-and-Cloud-SQL/) |
| Introductory | `GSP282` | [A Tour of Qwiklabs and Google Cloud](https://google.qwiklabs.com/focuses/2794?parent=catalog) | |
| Fundamental | `GSP407` | [Exploring Your Ecommerce Dataset with SQL in Google BigQuery](https://google.qwiklabs.com/focuses/3618?parent=catalog) | [EN](./normal-labs/GSP407_Exploring-Your-Ecommerce-Dataset-with-SQL-in-Google-BigQuery/) |
| Fundamental | `GSP408` | [Troubleshooting Common SQL Errors with BigQuery](https://google.qwiklabs.com/focuses/3642?parent=catalog) |  |
| Introductory | `GSP409` | [Explore and Create Reports with Data Studio](https://google.qwiklabs.com/focuses/3614?parent=catalog) |  |
| Fundamental | `GSP684` | [Compare Cloud AI Platform Models using the What-If Tool to Identify Potential Bias](https://google.qwiklabs.com/focuses/10605?parent=catalog) | [EN](./normal-labs/GSP684_Compare-Cloud-AI-Platform-Models-using-the-What-If-Tool-to-Identify-Potential-Bias/) |
| Fundamental | `GSP709` | [Identifying Bias in Mortgage Data using Cloud AI Platform and the What-if Tool](https://google.qwiklabs.com/focuses/10903?parent=catalog) | [EN](./normal-labs/GSP709_Identifying-Bias-in-Mortgage-Data-using-Cloud-AI-Platform-and-the-What-if-Tool/) |
| Fundamental | `GSP710` | [Using the What-If Tool with Image Recognition Models](https://google.qwiklabs.com/focuses/10904?parent=catalog) | [EN](./normal-labs/GSP710_Using-the-What-If-Tool-with-Image-Recognition-Models/) |

## FAQ

<details>
<summary>What's the difference between Quests and Skill Badges?</summary>

- `Quests = Group of Training Labs`  
  A self paced learning path which contains a collection of labs organized by technologies or specific cloud services
- `Skill Badges = Group of Training Labs + A Challenge Lab`  
  A self paced learning path which contains a collection of labs, however it capstones with a challenge lab.

</details>

## References

- [Adrianus Yoga | YouTube Channel](https://www.youtube.com/c/AdrianusYoga/videos)
- [Chris Research | YouTube Channel](https://www.youtube.com/c/chriskyfung-research)
- [Angga Agia Wardhana | YouTube Channel](https://www.youtube.com/c/anggaagia)
- [elmoallistair/qwiklabs](https://github.com/elmoallistair/qwiklabs)
- [DSC-IIIT-Kalyani/qwiklabs_challenges](https://github.com/DSC-IIIT-Kalyani/qwiklabs_challenges)
- [Qwiklabs : Lab Resources](https://docs.google.com/document/d/1B0iHlOd2LkuOW1j7dpfSW_GFAzR_jhUX-WnuqSwrXUA/edit)

## License

Licensed under the MIT License, Copyright © 2021-present Hsins.
