# GSP324 —— Explore Machine Learning Models with Explainable AI

<div align="center">
  <img src="https://i.imgur.com/F3iwIvo.png" alt="GSP324 —— Explore Machine Learning Models with Explainable AI">
</div>

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Challenge Scenario](#challenge-scenario)
- [Task 1: Start a JupyterLab Notebook instance](#task-1-start-a-jupyterlab-notebook-instance)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface)
- [Task 2: Download the Challenge Notebook](#task-2-download-the-challenge-notebook)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface-1)
- [Task 3: Build and train your models](#task-3-build-and-train-your-models)
  - [Description](#description)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface-2)
- [Task 4: Deploy the models to AI Platform](#task-4-deploy-the-models-to-ai-platform)
  - [Description](#description-1)
  - [Solution (Graphical User Interface)](#solution-graphical-user-interface-3)
- [[OPTIONAL] Task 05: Use the What-If Tool to explore biases](#optional-task-05-use-the-what-if-tool-to-explore-biases)
- [Review Questions](#review-questions)
- [References](#references)

</details>

<details>
  <summary>
    <strong>Quest Outline</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

| Level | Code | Name | Note |
| :--: | :--: | :-- | :--: |
| | VIDEO | [What is the What-If Tool?](https://www.youtube.com/watch?v=AX0KuRsFid8) |  |
| | VIDEO | [Getting Started with the What-if Tool](https://www.youtube.com/watch?v=qTUUwfG1vSs) |  |
| Introductory | `GSP076` | [AI Platform: Qwik Start](https://www.qwiklabs.com/focuses/581?parent=catalog) | [EN](../../normal-labs/GSP076_AI-Platform-Qwik-Start/) |
| Fundamental | `GSP710` | [Using the What-If Tool with Image Recognition Models](https://google.qwiklabs.com/focuses/10904?parent=catalog) | [EN](../../normal-labs/GSP710_Using-the-What-If-Tool-with-Image-Recognition-Models/) |
| | VIDEO | [Using the What-if Tool Performance & Fairness features](https://www.youtube.com/watch?v=ReqwELaX23I) |  |
| Fundamental | `GSP709` | [Identifying Bias in Mortgage Data using Cloud AI Platform and the What-if Tool](https://google.qwiklabs.com/focuses/10903?parent=catalog) | [EN](../../normal-labs/GSP709_Identifying-Bias-in-Mortgage-Data-using-Cloud-AI-Platform-and-the-What-if-Tool/) |
| Fundamental | `GSP684` | [Compare Cloud AI Platform Models using the What-If Tool to Identify Potential Bias](https://google.qwiklabs.com/focuses/10605?parent=catalog) | [EN](../../normal-labs/GSP684_Compare-Cloud-AI-Platform-Models-using-the-What-If-Tool-to-Identify-Potential-Bias/) |
| Advanced | `GSP324` | [Explore Machine Learning Models with Explainable AI: Challenge Lab](https://google.qwiklabs.com/focuses/12011?parent=catalog) |  |

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

## Task 2: Download the Challenge Notebook

### Solution (Graphical User Interface)

1. In the notebook, click the **terminal**.
2. Clone the repo with following command:

    ```bash
    $ git clone https://github.com/GoogleCloudPlatform/training-data-analyst
    ```

3. Open the notebook file `training-data-analyst/quests/dei/what-if-tool-challenge.ipynb`.
4. Run the cells to download and import the dataset `hmda_2017_ny_all-records_labels`.

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
    # Train your second model on the limited dataset.
    limited_model = Sequential()
    limited_model.add(layers.Dense(8, input_dim=input_size))
    limited_model.add(layers.Dense(1, activation='sigmoid'))
    limited_model.compile(optimizer='sgd', loss='mse')
    limited_model.fit(limited_train_data, limited_train_labels, batch_size=32, epochs=10)
    ```

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

Before deploy our modesl to the AI Platform, we have to create a Cloud Storage bucket for storing the models.

1. Click **Navigation Menu** > **Cloud Stroage** > **Browser**.
2. Click **CREATE BUCKET** and fill up the fields.
    - **Bucket Name**: use a globally unique name, e.g. `<Project_ID>`
3. Click **CREATE**

After created the bucket, switch back to the **JupyterLab** page and deploy models. Run the cells after modifing following part:

1. Define the environment variables in **Deploy your models to the AI Platform** section.

    ```python
    GCP_PROJECT = '<PROJECT_ID>'
    MODEL_BUCKET = 'gs://<BUCKET_NAME>' # recommend: as the same as the <PROJECT_ID>
    MODEL_NAME = 'complete_model'       # do not modify
    LIM_MODEL_NAME = 'limited_model'    # do not modify
    VERSION_NAME = 'v1'
    REGION = 'us-central1'
    ```

2. Add cells in **Create your first AI Platform model: `saved_complete_model`** section.

    ```python
    !gcloud ai-platform models create $MODEL_NAME --regions $REGION
    !gcloud ai-platform versions create $VERSION_NAME \
    --model=$MODEL_NAME \
    --framework='TensorFlow' \
    --runtime-version=2.3 \
    --origin=$MODEL_BUCKET/saved_complete_model \
    --staging-bucket=$MODEL_BUCKET \
    --python-version=3.7 \
    --project=$GCP_PROJECT
    ```

2. Add cells in **Create your second AI Platform model: `saved_limited_model`** section.

    ```python
    !gcloud ai-platform models create $LIM_MODEL_NAME --regions $REGION
    !gcloud ai-platform versions create $VERSION_NAME \
    --model=$LIM_MODEL_NAME \
    --framework='TensorFlow' \
    --runtime-version=2.3 \
    --origin=$MODEL_BUCKET/saved_limited_model \
    --staging-bucket=$MODEL_BUCKET \
    --python-version=3.7 \
    --project=$GCP_PROJECT
    ```

## [OPTIONAL] Task 05: Use the What-If Tool to explore biases

After the models are deployed to the AI Platform, we can use the following code to explore them in the What-If Tool in the notebook.

```python
config_builder = (WitConfigBuilder(
    examples_for_wit[:num_datapoints],feature_names=column_names)
    .set_custom_predict_fn(limited_custom_predict)
    .set_target_feature('loan_granted')
    .set_label_vocab(['denied', 'accepted'])
    .set_compare_custom_predict_fn(custom_predict)
    .set_model_name('limited')
    .set_compare_model_name('complete'))
WitWidget(config_builder, height=800)
```

## Review Questions

1. In the Performance and Fairness tab, slice by sex (`applicant_sex_name_Female`). How does the complete model compare to the limited model for females?

    > The complete model has equal performance accross sexes, whereas the limited model is much worse on females.

2. Click on one of the datapoints in the middle of the arc. In the datapoint editor, change `(applicant_sex_name_Female)` to `0`, and `(applicant_sex_name_Male)` to `1`. Now run the inference again. How does the model change?

    > The limited model has a significantly larger delta than the complete model, whereas the complete model has almost no change.

3. In the Performance and Fairness tab, use the fairness buttons to see the thresholds for the sexes for demographic parity between males and females. How does this change the thresholds for the limited model?

    > The thresholds have to be wildly different for the limited model.

## References

- [`tf.keras.Sequential` | TensorFlow Core Documentation](https://www.tensorflow.org/api_docs/python/tf/keras/Sequential)
