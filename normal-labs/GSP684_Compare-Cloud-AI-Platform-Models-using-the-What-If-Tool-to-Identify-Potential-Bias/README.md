# GSP684 —— Compare Cloud AI Platform Models using the What-If Tool to Identify Potential Bias

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Deploy Models to AI Platform](#deploy-models-to-ai-platform)
- [References](#references)

</details>

## Overview

In this lab, you deploy two models on Cloud AI Platform, and then use the What-If Tool to identify potential bias in the models and underlying dataset. You will have the opportunity to address identified bias, retrain the models, redeploy them, and continue to compare them with the What-If Tool.

Objectives:

- Train tf.keras and Scikit Learn models in Cloud AI Platform Notebooks.
- Deploy models to AI Platform Predictions.
- Use the What-If Tool to analyze and compare the models.

## Deploy Models to AI Platform

```bash
# create a model
$ gcloud ai-platform models create <MODEL_NAME> --regions=<REGION>

# create a version
$ gcloud ai-platform versions create <VRESION_NAME> \
    --model=<MODEL_NAME> \
    --framework=<FRAMEWORK> \
    --runtime-version=<RUNTIME_VERSION> \
    --origin=<MODEL_BUCKET> \
    --staging-bucket=<MODEL_BUCKET> \
    --python-version=<PYTHON-VERSION> \
    --project=<PROJECT> \
    --region=<REGION>
```

## References

- [What-If Tool](https://pair-code.github.io/what-if-tool/)
- [AI Platform Documentation](https://cloud.google.com/ai-platform/prediction/docs/using-what-if-tool)
- [GoogleCloudPlatform/training-data-analyst | GitHub](https://github.com/GoogleCloudPlatform/training-data-analyst): `training-data-analyst/quests/dei/census/income_xgboost.ipynb`