# Google Cloud Platform (GCP) Cheatsheet

- [Google Cloud Platform (GCP) Cheatsheet](#google-cloud-platform-gcp-cheatsheet)
  - [Environment Variables](#environment-variables)
  - [Regions and Zones](#regions-and-zones)
  - [COMPUTE](#compute)
    - [Cloud Functions](#cloud-functions)
  - [STORAGE](#storage)
    - [Cloud Storages](#cloud-storages)
  - [DATABASES](#databases)
  - [NETWORKING](#networking)
  - [OPERATIONS](#operations)
  - [BIG DATA](#big-data)
    - [BigQuery](#bigquery)
  - [References](#references)

## Environment Variables

```bash
$ echo "$DEVSHELL_PROJECT_ID"
```

## Regions and Zones

```bash
# list all zones
$ gcloud compute zones list
```

## COMPUTE

### Cloud Functions

```bash
# create and deploy function
$ gcloud functions deploy <FUNCTION-NAME> \
  --stage-bucket=<STAGE-BUCKET> \
  --trigger-topic=<TRIGGER-TOPIC> \
  --runtime=<RUNTIME>

# verify status of function
$ gcloud functions describe <FUNCTION-NAME>

# create test of function
$ gcloud functions call <FUNCTION-NAME> --data <DATA>

# check logs in the log history
$ gcloud functions logs read <FUNCTION-NAME>
```

## STORAGE

### Cloud Storages

```bash
# list all buckets
$ gsutil ls

# upload file
$ gsutil cp <FILE_NAME> gs://<BUCKET_NAME>/<DIR_PATH>/

# delete file
$ gsutil rm gs://<BUCKET_NAME>/<FILE_PATH>

# download file
$ gsutil cp gs://<BUCKET_NAME>/<FILE_PATH> .

# move file
$ gsutil mv <SRC_FILE_PATH> gs://<BUCKET_NAME>/<DEST_FILE_PATH>
```

## DATABASES

## NETWORKING

## OPERATIONS

## BIG DATA

### BigQuery

```bash
# list any existing datasets in our project
$ bq ls

# create dataset
$ bq mk <DATASET_NAME>

# remove dataset
$ bq rm -r <DATASET>

# create or update table and load data
$ bq load <DATASET:TABLE> <FILE> <SCHEMA>

# check the schema of given table
$ bq show <DATASET:TABLE>

# examing schema of given table
$ bq show <PROJECT>:<DATASET.TABLE>

# run query
$ bq query "[SQL_STATEMENT]"
```

## References