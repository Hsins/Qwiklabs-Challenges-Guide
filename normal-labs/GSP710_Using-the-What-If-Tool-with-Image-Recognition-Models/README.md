# GSP710 —— Using the What-If Tool with Image Recognition Models

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [What-If Tool](#what-if-tool)
- [References](#references)

</details>

## Overview

In this lab, you explore the use of the What-If Tool (WIT) for image recognition models. Your task is to predict whether a person is smiling. The lab provides a CNN (Convolutional Neural Network) that is trained on a subset of [CelebA dataset](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html) and visualizes the results on a separate test subset.

Objectives:

- Launch an AI Platform Notebook.
- Download the pre-trained Keras model.
- Define helper functions for dataset conversion from csv to tf.
- Load the csv file into pandas dataframe and process it for WIT.
- Load the Keras models.
- Define the custom predict function for WIT.

## What-If Tool

We can use the What-If Tool (WIT) within notebook environments to inspect AI Platform Prediction models through an interactive dashboard.

- An extension in Jupyter, Colaboratory, and Cloud AI Platform notebooks.
- Integrates with TensorBoard, Jupyter notebooks, Colab notebooks, and JupyterHub.
- Pre-installed on Notebooks TensorFlow instances.
- Used to analyze classification or regression models on datapoints as inputs directly from within the notebook.

## References

- [What-If Tool](https://pair-code.github.io/what-if-tool/)
- [AI Platform Documentation](https://cloud.google.com/ai-platform/prediction/docs/using-what-if-tool)
- [GoogleCloudPlatform/training-data-analyst | GitHub](https://github.com/GoogleCloudPlatform/training-data-analyst)