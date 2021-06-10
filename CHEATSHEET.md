# Google Cloud Platform (GCP) Cheatsheet

- [Google Cloud Platform (GCP) Cheatsheet](#google-cloud-platform-gcp-cheatsheet)
  - [Regions and Zones](#regions-and-zones)
  - [Storages and Buckets](#storages-and-buckets)
  - [References](#references)

## Regions and Zones

```bash
# list all zones
$ gcloud compute zones list
```

## Storages and Buckets

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

## References