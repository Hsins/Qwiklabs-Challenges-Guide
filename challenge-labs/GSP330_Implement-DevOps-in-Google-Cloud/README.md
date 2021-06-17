# GSP330 —— Implement DevOps in Google Cloud

<div align="center">
  <img src="https://i.imgur.com/F3iwIvo.png" alt="GSP330 —— Implement DevOps in Google Cloud">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP330 —— Implement DevOps in Google Cloud](#gsp330--implement-devops-in-google-cloud)
  - [Overview](#overview)
  - [Challenge Scenario](#challenge-scenario)
  - [Task 1: Start a JupyterLab Notebook instance](#task-1-start-a-jupyterlab-notebook-instance)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface)
    - [References](#references)
  - [Task 2: Download the Challenge Notebook](#task-2-download-the-challenge-notebook)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface-1)
    - [References](#references-1)
  - [Task 3: Build and train your models](#task-3-build-and-train-your-models)
    - [Description](#description)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface-2)
    - [References](#references-2)
  - [Task 4: Deploy the models to AI Platform](#task-4-deploy-the-models-to-ai-platform)
    - [Description](#description-1)
    - [Solution (Graphical User Interface)](#solution-graphical-user-interface-3)
    - [References](#references-3)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| | VIDEO | [Why you should read DORA’s 2019 Accelerate State of DevOps Report](https://www.youtube.com/watch?v=8M3WibXvC84) |  |
| Introductory | `GSP121` | [Cloud Source Repositories: Qwik Start](https://www.qwiklabs.com/focuses/1002?parent=catalog) | [EN](../../normal-labs/GSP121_Cloud-Source-Repositories-Qwik-Start/) |
| Advanced | `GSP053` | [Managing Deployments Using Kubernetes Engine](https://www.qwiklabs.com/focuses/639?parent=catalog) | [EN]() |
| Advanced | `GSP233` | [Deploy Kubernetes Load Balancer Service with Terraform](https://www.qwiklabs.com/focuses/1205?parent=catalog) | [EN]() |
| Advanced | `GSP425` | [Site Reliability Troubleshooting with Cloud Monitoring APM](https://www.qwiklabs.com/focuses/4186?parent=catalog) | [EN]() |
| Advanced | `GSP051` | [Continuous Delivery with Jenkins in Kubernetes Engine](https://www.qwiklabs.com/focuses/1104?parent=catalog) | [EN]() |
| Expert | `` | [Implement DevOps in Google Cloud: Challenge Lab](https://google.qwiklabs.com/focuses/0?parent=catalog) |  |

</details>

## Overview

This lab is recommended for students who have enrolled in the [Explore Machine Learning Models with Explainable AI](https://google.qwiklabs.com/quests/126) quest.

Topics tested:

- Launching an AI Platform Notebook
- Downloading and exploring a sample dataset
- Building and training two different TensorFlow models
- Deploying models to the Cloud AI Platform
- Using the What-If Tool to compare the models

## Challenge Scenario

You are a curious coder who wants to explore biases in public datasets using the What-If Tool. You decide to pull some mortgage [data](https://www.consumerfinance.gov/data-research/hmda/historic-data/) to train a couple of machine learning models to predict whether an applicant will be granted a loan. You specifically want to investigate how the two models perform when they are trained on different proportions of males and females in the datasets, and visualize their differences in the What-If Tool.

You are expected to have the skills and knowledge for these tasks, so don’t expect step-by-step guides.

## Task 1: Start a JupyterLab Notebook instance

### Solution (Graphical User Interface)

1. Click **Navigation Menu** > **AI Platform** > **Notebooks**.
2. In the Notebooks Instance page, click **NEW INSTANCE**.
3. In the Customize instance menu, select the version of notebook instance.
    - **TensorFlow Enterprise 2.3** > **Without GPUs**.
    - Region: `us-central1 (Iowa)`
4. Click **CREATE**, the AI Platform console will display your instance name after a few minutes.
5. Click **OPEN JUPYTERLAB**. Your notebook is now set up.

> A notification should pop up asking you to migrate your notebook instance to the new Notebooks API. Click Enable Notebooks API to give your notebook additional functionality.

### References

## Task 2: Download the Challenge Notebook

### Solution (Graphical User Interface)

1. In the notebook, click the **terminal**.
2. Clone the repo with following command:

    ```bash
    $ git clone https://github.com/GoogleCloudPlatform/training-data-analyst
    ```

3. Open the notebook file `training-data-analyst/quests/dei/what-if-tool-challenge.ipynb`.
4. Run the cells to download and import the dataset `hmda_2017_ny_all-records_labels`.

### References

## Task 3: Build and train your models

### Description

Use TensorFlow to build two models: one trained on the complete dataset, and one trained on the limited dataset. You should use the model `Sequential()`. Documentation is [here](https://www.tensorflow.org/api_docs/python/tf/keras/Sequential).

**IMPORTANT**: To accurately check your progress, the first model should be saved in the location saved_complete_model/saved_model.pb and the second in saved_limited_model/saved_model.pb.

### Solution (Graphical User Interface)

1. Navigate to the **Create and train your TensorFlow models** section in notebook.
2. Train the first model with following code:

    ```python
    # Train the first model on the complete dataset.
    model = Sequential()
    model.add(layers.Dense(8, input_dim=input_size))
    model.add(layers.Dense(1, activation='sigmoid'))
    model.compile(optimizer='sgd', loss='mse')
    model.fit(train_data, train_labels, batch_size=32, epochs=10)
    ```

3. Train the second model with following code:

    ```python
    # Train your second model on the limited dataset. Use `limited_train_data` for your data and `limited_train_labels` for your labels.
    limited_model = Sequential()
    limited_model.add(layers.Dense(8, input_dim=input_size))
    limited_model.add(layers.Dense(1, activation='sigmoid'))
    limited_model.compile(optimizer='sgd', loss='mse')
    limited_model.fit(limited_train_data, limited_train_labels, batch_size=32, epochs=10)
    ```

### References

- [`tf.keras.Sequential` | TensorFlow Core Documentation](https://www.tensorflow.org/api_docs/python/tf/keras/Sequential)

## Task 4: Deploy the models to AI Platform

### Description

Now, you'll deploy your models to the AI Platform.

**Hint**: You need to first create a storage bucket to store your models in.

- Create the Complete AI Platform model
  - Model Name = `complete_model`
  - Version Name = v1
  - Python version = 3.7
  - Framework = TensorFlow
  - Framework version = 2.3.1
  - ML Runtime version = 2.3
- Create the Limited AI Platform model
  - Model Name = `limited_model`
  - Version Name = v1
  - Python version = 3.7
  - Framework = TensorFlow
  - Framework version = 2.3.1
  - ML Runtime version = 2.3

### Solution (Graphical User Interface)

1. Create Cloud Storage bucket.
2. Fill out information.

Create the Complete AI Platform model:

```bash
$ gcloud ai-platform models create $MODEL_NAME --regions $REGION
$ gcloud ai-platform versions create $VERSION_NAME \
    --model=$MODEL_NAME \
    --framework='TensorFlow' \
    --runtime-version=2.3 \
    --origin=$MODEL_BUCKET/saved_complete_model \
    --staging-bucket=$MODEL_BUCKET \
    --python-version=3.7 \
    --project=$GCP_PROJECT
```

Create the Limited AI Platform model:

```bash
$ gcloud ai-platform models create $LIM_MODEL_NAME --regions $REGION
$ gcloud ai-platform versions create $VERSION_NAME \
    --model=$LIM_MODEL_NAME \
    --framework='TensorFlow' \
    --runtime-version=2.3 \
    --origin=$MODEL_BUCKET/saved_limited_model \
    --staging-bucket=$MODEL_BUCKET \
    --python-version=3.7 \
    --project=$GCP_PROJECT
```

### References