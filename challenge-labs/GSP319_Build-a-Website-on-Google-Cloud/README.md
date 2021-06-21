# GSP319 —— Build a Website on Google Cloud

<div align="center">
  <img src="https://i.imgur.com/PVS5Uso.png" alt="GSP313 —— Create and Manage Cloud Resources">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Challenge Scenario](#challenge-scenario)
- [Task 1: Download the monolith code and build your container](#task-1-download-the-monolith-code-and-build-your-container)
  - [Description](#description)
  - [Solution (Command Line Interface)](#solution-command-line-interface)
- [Task 2: Create a kubernetes cluster and deploy the application](#task-2-create-a-kubernetes-cluster-and-deploy-the-application)
  - [Description](#description-1)
  - [Solution (Command Line Interface)](#solution-command-line-interface-1)
- [Task 3: Create a containerized version of your Microservices](#task-3-create-a-containerized-version-of-your-microservices)
  - [Description](#description-2)
  - [Solution (Command Line Interface)](#solution-command-line-interface-2)
- [Task 4: Deploy the new microservices](#task-4-deploy-the-new-microservices)
  - [Description](#description-3)
  - [Solution (Command Line Interface)](#solution-command-line-interface-3)
- [Task 5: Configure the Frontend microservice](#task-5-configure-the-frontend-microservice)
  - [Description](#description-4)
  - [Solution (Command Line Interface)](#solution-command-line-interface-4)
- [Task 6: Create a containerized version of the Frontend microservice](#task-6-create-a-containerized-version-of-the-frontend-microservice)
  - [Description](#description-5)
  - [Solution (Command Line Interface)](#solution-command-line-interface-5)
- [Task 7: Deploy the Frontend microservice](#task-7-deploy-the-frontend-microservice)
  - [Description](#description-6)
  - [Solution (Command Line Interface)](#solution-command-line-interface-6)
- [References](#references)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| | VIDEO | [Hosting a static web app on Google Cloud using GCS](https://www.youtube.com/watch?v=HkJxy22P5gk) |  |
| Fundamental | `GSP659` | [Deploy Your Website on Cloud Run](https://google.qwiklabs.com/focuses/10445?parent=catalog) | [EN](../../normal-labs/GSP659_Deploy-Your-Website-on-Cloud-Run/) |
| | VIDEO | [Hosting a web app on Google Cloud using GCE](https://www.youtube.com/watch?v=nnXi0ABwSXA) |  |
| Fundamental | `GSP662` | [Hosting a Web App on Google Cloud Using Compute Engine](https://google.qwiklabs.com/focuses/11952?parent=catalog) | [EN](../../normal-labs/GSP662_Hosting-a-Web-App-on-Google-Cloud-Using-Compute-Engine/) |
| Fundamental | `GSP663` | [Deploy, Scale, and Update Your Website on Google Kubernetes Engine](https://google.qwiklabs.com/focuses/10470?parent=catalog) | [EN](../../normal-labs/GSP663_Deploy-Scale-and-Update-Your-Website-on-Google-Kubernetes-Engine/) |
| Advanced | `GSP699` | [Migrating a Monolithic Website to Microservices on Google Kubernetes Engine](https://google.qwiklabs.com/focuses/11953?parent=catalog) | [EN](../../normal-labs/GSP699_Migrating-a-Monolithic-Website-to-Microservices-on-Google-Kubernetes-Engine/) |
| | VIDEO | [Case Study: Hosting Scalable web apps on Google Cloud](https://www.youtube.com/watch?v=tts41rFP_0k) |  |
| Advanced | `GSP319` | [Build a Website on Google Cloud: Challenge Lab](https://google.qwiklabs.com/focuses/11765?parent=catalog) |  |


</details>

## Overview

This lab is recommended for students who have enrolled in the [Build a Website on Google Cloud](https://google.qwiklabs.com/quests/115) quest.

Topics tested:

- Building and refactoring a monolithic web app into microservices
- Deploying microservices in GKE
- Exposing the Services deployed on GKE

## Challenge Scenario

You have just started a new role at FancyStore, Inc.

Your task is to take the company's existing monolithic e-commerce website and break it into a series of logically separated microservices. The existing monolith code is sitting in a GitHub repo, and you will be expected to containerize this app and then refactor it.

You are expected to have the skills and knowledge for these tasks, so don't expect step-by-step guides.

You have been asked to take the lead on this, after the last team suffered from monolith-related burnout and left for greener pastures (literally, they are running a lavender farm now). You will be tasked with pulling down the source code, building a container from it (one of the farmers left you a Dockerfile), and then pushing it out to GKE.

You should first build, deploy, and test the Monolith, just to make sure that the source code is sound. After that, you should break out the constituent services into their own microservice deployments.

Some FancyStore, Inc. standards you should follow:

- Create your cluster in `us-central-1`.
- Naming is normally `team-resource`, e.g. an instance could be named `fancystore-orderservice1`.
- Allocate cost effective resource sizes. Projects are monitored and excessive resource use will result in the containing project's termination.
- Use the `n1-standard-1` machine type unless directed otherwise.

## Task 1: Download the monolith code and build your container

### Description

Log in to your new project, open up Cloud Shell.

First things first, you'll need to [clone your team's git repo](https://github.com/googlecodelabs/monolith-to-microservices). There's a setup.sh script in the root directory of the project that you'll need to run to get your monolith container built up.

After running the `setup.sh` script, there will be a few different projects that can be built and pushed.

Push the monolith build (conveniently located in the `monolith` directory) up to the Google Container Registry. There's a Dockerfile located in the `~/monotlith-to-microservices/monolith` folder which you can use to build the application container.

You will have to run Cloud Build (in that monolith folder) to build it, then push it up to GCR.

Name your artifact as follows:

```
GCR Repo: gcr.io/${GOOGLE_CLOUD_PROJECT}
Image name: fancytest
Image version: 1.0.0
```

**Hint**:

Make sure that you submit a build named "fancytest" with a version of "1.0.0".

### Solution (Command Line Interface)

```bash
# clone the repository
$ git clone https://github.com/googlecodelabs/monolith-to-microservices.git

# install dependencies
$ cd ~/monolith-to-microservices
$ ./setup.sh

# enable the Cloud Build API and submit the docker container
$ cd ~/monolith-to-microservices/monolith
$ gcloud services enable cloudbuild.googleapis.com
$ gcloud builds submit --tag="gcr.io/${GOOGLE_CLOUD_PROJECT}/fancytest:1.0.0" .
```

## Task 2: Create a kubernetes cluster and deploy the application

### Description

Now that you have the image created and sitting in the container registry, it's time to create a cluster to deploy it to.

You've been told to deploy all of your resources in the `us-central1-a` zone, so first you'll need to create a GKE cluster for it. Start with a 3 node cluster to begin with.

Create your cluster as follows:

```
Cluster name: fancy-cluster
Region: us-central1-a
Node count: 3
```

**Hint**:

Make sure your cluster is named "fancy-cluster", and is in the running state in `us-central1-a`.

Now that you've built up an image, and have a cluster up and running, it's time to deploy your application.

You'll need to deploy the image that you've built onto your cluster. This will get your application up and running, but it can't be accessed until you expose it to the outside world. Your team has told you that the application runs on port 8080, but you will need to expose this on a more consumer-friendly port 80.

Create and expose your deployment as follows:

```
Cluster name: fancy-cluster
Container name: fancytest
Container version: 1.0.0
Application port: 8080
Externally accessible port: 80
```

**Hint**:

Make sure your deployment is named `"fancytest"`, and that you have exposed the service on port `80`, and mapped it to port `8080`.

### Solution (Command Line Interface)

```bash
# setup the default zone
$ gcloud config set compute/zone us-central1-a

# enable the Cloud Build API and create the Kubernetes cluster
$ gcloud services enable container.googleapis.com
$ gcloud container clusters create fancy-cluster --num-nodes 3

# deploy application to the cluster
$ kubectl create deployment fancytest \
    --image="gcr.io/${GOOGLE_CLOUD_PROJECT}/fancytest:1.0.0"

# expose the service port
$ kubectl expose deployment fancytest \
    --type="LoadBalancer" \
    --port=80 --target-port=8080
```

## Task 3: Create a containerized version of your Microservices

### Description

Below is the set of services which need to be containerized. Navigate to the source roots mentioned below, and upload the artifacts which are created to the Google Container Registry with the metadata indicated.

<details>
  <summary>
    <strong>Orders Microservice</strong>
  </summary>

```
Service root folder: ~/monolith-to-microservices/microservices/src/orders
GCR Repo: gcr.io/${GOOGLE_CLOUD_PROJECT}
Image name: orders
Image version: 1.0.0
```

</details>

<details>
  <summary>
    <strong>Products Microservice</strong>
  </summary>

```
Service root folder: ~/monolith-to-microservices/microservices/src/products
GCR Repo: gcr.io/${GOOGLE_CLOUD_PROJECT}
Image name: products
Image version: 1.0.0
```

</details>

Once these microservices have been containerized, and their images uploaded to the GCR, you should deploy and expose these services.

**Hint**: Make sure that you submit a build named `"orders"` with a version of `"1.0.0"`, AND a build named `"products"` with a version of `"1.0.0"`.

### Solution (Command Line Interface)

```bash
# navigate to target folder and build the Docker container: orders
$ cd ~/monolith-to-microservices/microservices/src/orders
$ gcloud builds submit --tag="gcr.io/${GOOGLE_CLOUD_PROJECT}/orders:1.0.0" .

# navigate to target folder and build the Docker container: products
$ cd ~/monolith-to-microservices/microservices/src/products
$ gcloud builds submit --tag="gcr.io/${GOOGLE_CLOUD_PROJECT}/products:1.0.0" .
```

## Task 4: Deploy the new microservices

### Description

Deploy these new containers following the same process that you followed for the "fancytest" monolith. Note that these services will be listening on different ports, so make note of the port mappings in the table below.

Create and expose your deployments as follows:

<details>
  <summary>
    <strong>Orders Microservice</strong>
  </summary>

```
Cluster name: fancy-cluster
Container name: orders
Container version: 1.0.0
Application port: 8081
Externally accessible port: 80
```

</details>

<details>
  <summary>
    <strong>Products Microservice</strong>
  </summary>

```
Cluster name: fancy-cluster
Container name: products
Container version: 1.0.0
Application port: 8082
Externally accessible port: 80
```

</details>

**NOTE**: Please make note of the IP address of both the Orders and Products services once they have been exposed, you will need them in future steps.

You can verify that the deployments were successful and that the services have been exposed by going to the following URLs in your browser:

- `http://ORDERS_EXTERNAL_IP/api/orders`

- `http://PRODUCTS_EXTERNAL_IP/api/products`

You will see each service return a JSON string if the deployments were successful.

**Hint**: Make sure your deployments are named `"orders"` and `"products"`, and that you see the services exposed on port `80`.

### Solution (Command Line Interface)

```bash
# deploy the Orders Microservice and expose the service on port 80
$ kubectl create deployment orders --image="gcr.io/${GOOGLE_CLOUD_PROJECT}/orders:1.0.0"
$ kubectl expose deployment orders --type="LoadBalancer" --port=80 --target-port=8081

# deploy the Products Microservice and expose the service on port 80
$ kubectl create deployment products --image="gcr.io/${GOOGLE_CLOUD_PROJECT}/products:1.0.0"
$ kubectl expose deployment products --type="LoadBalancer" --port=80 --target-port=8082
```

## Task 5: Configure the Frontend microservice

### Description

Replace the local URL with the IP address of the new Products microservices and rebuild the frontend application before containerizing it.

### Solution (Command Line Interface)

```bash
# check the external IP of services
$ kubectl get service

# set the environment variables
$ ORDERS_IP_ADDRESS=$(kubectl get services orders --output jsonpath='{.status.loadBalancer.ingress[0].ip}')
$ PRODUCTS_IP_ADDRESS=$(kubectl get services products --output jsonpath='{.status.loadBalancer.ingress[0].ip}')

# replace the IP address in .env file and build again
$ cd ~/monolith-to-microservices/react-app
$ sed "s/localhost\:8081/$ORDERS_IP_ADDRESS/g" -i .env
$ sed "s/localhost\:8082/$PRODUCTS_IP_ADDRESS/g" -i .env
$ npm run build
```

## Task 6: Create a containerized version of the Frontend microservice

### Description

With the Orders and Products microservices now containerized and deployed, and the Frontend service configured to point to them, the final step is to containerize and deploy the Frontend.

Use Cloud Build to package up the contents of the Frontend service and push it up to the Google Container Registry.

```
Service root folder:  ~/monolith-to-microservices/microservices/src/frontend
GCR Repo: gcr.io/${GOOGLE_CLOUD_PROJECT}
Image name: frontend
Image version: 1.0.0
This process may take a few minutes, so be patient.
```

**Hint**: Make sure that you submit a build named `"frontend"` with a version of `"1.0.0"`.

### Solution (Command Line Interface)

```bash
$ cd ~/monolith-to-microservices/microservices/src/frontend
$ gcloud builds submit --tag="gcr.io/${GOOGLE_CLOUD_PROJECT}/frontend:1.0.0" .
```

## Task 7: Deploy the Frontend microservice

### Description

Deploy this container following the same process that you followed for the "Orders" and "Products" microservices.

Create and expose your deployment as follows:

```
Cluster name: fancy-cluster
Container name: frontend
Container version: 1.0.0
Application port: 8080
Externally accessible port: 80
```

You can verify that the deployment was successful and that the microservices have been properly exposed by hitting the following the IP address of the frontend service in your browser: You will see the Fancy Store homepage, with links to the Products and Orders pages powered by your new microservices.

### Solution (Command Line Interface)

```bash
# deploy the Frontend Microservice and expose the service on port 80
$ kubectl create deployment frontend --image="gcr.io/${GOOGLE_CLOUD_PROJECT}/frontend:1.0.0"
$ kubectl expose deployment frontend --type="LoadBalancer" --port=80 --target-port=8080
```

## References

- [googlecodelabs/monolith-to-microservices | GitHub](https://github.com/googlecodelabs/monolith-to-microservices)
- [Best practices for microservices | Cloud Architecture Center](https://cloud.google.com/solutions/migrating-a-monolithic-app-to-microservices-gke#best_practices_for_microservices)