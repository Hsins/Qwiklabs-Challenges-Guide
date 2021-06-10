# GSP074 —— Cloud Storage: Qwik Start - CLI/SDK

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Create Buckets](#create-buckets)
- [Objects CRUD](#objects-crud)
- [Share Objects Publicly](#share-objects-publicly)
- [References](#references)

</details>

## Overview

Cloud Storage allows world-wide storage and retrieval of any amount of data at any time. You can use Cloud Storage for a range of scenarios including serving website content, storing data for archival and disaster recovery, or distributing large data objects to users via direct download.

In this hands-on lab you will learn how to create a storage bucket, upload objects to it, create folders and subfolders in it, and make objects publicly accessible using the Google Cloud command line.

Throughout this lab you'll be able to verify your work in the Console by going to Navigation menu > Storage. You'll just need to refresh your browser after each command is run to see the new items you've created.

## Create Buckets

```bash
$ gsutil mb -p <PROJECT_ID> -c <STORAGE_CLASS> -l <BUCKET_LOCATION> -b on gs://<BUCKET_NAME>
```

There're the Bucket naming rules:

- Do not include sensitive information in the bucket name, because **the bucket namespace is global and publicly visible**.
- Bucket names must contain only lowercase letters, numbers, dashes (-), underscores (`_`), and dots (`.`). Names containing dots require [verification](https://cloud.google.com/storage/docs/domain-name-verification).
- Bucket names must start and end with a number or letter.
- Bucket names must contain 3 to 63 characters. Names containing dots can contain up to 222 characters, but each dot-separated component can be no longer than 63 characters.
- Bucket names cannot be represented as an IP address in dotted-decimal notation (for example, `192.168.5.4`).
- Bucket names cannot begin with the `"goog"` prefix.
- Bucket names cannot contain `"google"` or close misspellings of `"google"`.
- For DNS compliance and future compatibility, you should not use underscores (`_`) or have a period adjacent to another period or dash. For example, "`..`" or "`-.`" or "`.-`" are not valid in DNS names.


## Objects CRUD

```bash
# upload files
$ gsutil cp <FILE-NAME> gs://<YOUR-BUCKET-NAME>
$ gsutil cp <FILE-NAME> gs://<YOUR-BUCKET-NAME>/<FOLDER-NAME>/  # create folder and copy files into

# download files
$ gsutil cp -r gs://<YOUR-BUCKET-NAME>/<FILE-NAME> .

# list the contents of the bucket
$ gsutil ls gs://<YOUR-BUCKET-NAME>

# get details about the file
$ gsutil ls -l gs://<YOUR-BUCKET-NAME>/<FILE-NAME>

# delete objects
$ gsutil rm gs://<YOUR-BUCKET-NAME>/<FILE-NAME>
```

## Share Objects Publicly

```bash
# grant permission for the objects
$ gsutil acl ch -u <ID>|<EMAIL>:<PERMISSION> gs://<YOUR-BUCKET-NAME>/<FILE-NAME>

# remove permission for the objects
$ gsutil acl ch -d <ID>|<EMAIL>|<DOMAIN>|All|AllAuth|(viewers|editors|owners)-<PROJECT-NUMBER> gs://<YOUR-BUCKET-NAME>/<FILE-NAME>
```

## References

- [Cloud Storage Documentation](https://cloud.google.com/storage/docs)
- [Google Cloud Storage: Massive Scalability Plus More | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=081hh6EzlTk)
- [`mb` - Make buckets | Cloud Storage Documentation](https://cloud.google.com/storage/docs/gsutil/commands/mb)
- [`cp` - Copy files and objects | Cloud Storage Documentation](https://cloud.google.com/storage/docs/gsutil/commands/cp)
- [`ls` - List providers, buckets, or objects | Cloud Storage Documentation](https://cloud.google.com/storage/docs/gsutil/commands/ls)
- [`acl` - Get, set, or change bucket and/or object ACLs | Cloud Storage Documentation](https://cloud.google.com/storage/docs/gsutil/commands/acl)
- [`rm` - Remove objects | Cloud Storage Documentation](https://cloud.google.com/storage/docs/gsutil/commands/rm)