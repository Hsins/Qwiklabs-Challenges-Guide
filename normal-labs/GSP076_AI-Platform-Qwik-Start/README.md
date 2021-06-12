# GSP076 —— AI Platform: Qwik Start

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Goals](#goals)
- [Launch AI Platform Notebooks](#launch-ai-platform-notebooks)
- [References](#references)

</details>

## Overview

This lab will give you hands-on practice with [TensorFlow 2.x](https://www.tensorflow.org/) model training, both locally and on [AI Platform](https://cloud.google.com/ai-platform/docs/). After training, you will learn how to deploy your model to AI Platform for serving (prediction). You'll train your model to predict income category of a person using the [United States Census Income Dataset](https://archive.ics.uci.edu/ml/datasets/Census+Income).

This lab gives you an introductory, end-to-end experience of training and prediction on AI Platform. The lab will use a census dataset to:

- Create a TensorFlow 2.x training application and validate it locally.
- Run your training job on a single worker instance in the cloud.
- Deploy a model to support prediction.
- Request an online prediction and see the response.

## Goals

The sample builds a classification model for predicting income category based on United States Census Income Dataset. The two income categories (also known as labels) are:

- **>50K** — Greater than 50,000 dollars
- **<=50K** — Less than or equal to 50,000 dollars

The sample defines the model using the Keras Sequential API. The sample defines the data transformations particular to the census dataset, then assigns these (potentially) transformed features to either the DNN or the linear portion of the model.

## Launch AI Platform Notebooks

1. Click **Navigation Menu** > **AI Platform** > **Notebooks**.
2. On the **Notebook Instances** page, click **New Instance**.
3. In the pop-up dialog, confirm the fields and click **Create**.
4. Click **Open JupyterLab**. A JupyterLab window will open in a new tab.

## References

- [What is Machine Learning? | YouTube](https://www.youtube.com/watch?v=HcqpanDadyQ)
- [Harness the Power of Machine Learning with Cloud ML Engine | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=m0rqccviLNM)
- [Cloud ML Engine: Qwik Start - Qwiklabs Preview | YouTube](https://www.youtube.com/watch?v=ZhQK0glTLg0)
- [GoogleCloudPlatform/training-data-analyst | GitHub](https://github.com/GoogleCloudPlatform/training-data-analyst)