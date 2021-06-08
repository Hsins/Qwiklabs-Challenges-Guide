# Google Cloud Platform (GCP) Cheatsheet

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
$ gsutil cp <FILENAME> gs://<bucket-name>/<directory>/

# delete file
$ gsutil rm gs://<bucket-name>/<filepath>

# download file
$ gsutil cp gs://<bucket-name>/<dir-path>/package-1.1.tgz .

# move file
$ gsutil mv <src-filepath> gs://<bucket-name>/<directory>/<dest-filepath>
```