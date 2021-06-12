# GSP709 —— Identifying Bias in Mortgage Data using Cloud AI Platform and the What-if Tool

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Deploy Models to AI Platform](#deploy-models-to-ai-platform)
- [Using the What-if Tool to Interpret Model](#using-the-what-if-tool-to-interpret-model)
- [References](#references)

</details>

## Overview

In this lab, you use the What-If Tool to identify potential biases in a model that was trained on a mortgage loan applications dataset.

Objectives:

- Build a binary classification model using XGBoost.
- Deploy the model to Cloud AI Platform.
- Use the What-If Tool on the deployed model to search for biases.

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
- [GoogleCloudPlatform/training-data-analyst | GitHub](https://github.com/GoogleCloudPlatform/training-data-analyst)