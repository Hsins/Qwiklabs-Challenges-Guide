# GSP073 —— Cloud Storage: Qwik Start - Cloud Console

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP073 —— Cloud Storage: Qwik Start - Cloud Console](#gsp073--cloud-storage-qwik-start---cloud-console)
  - [Overview](#overview)
  - [Create Buckets](#create-buckets)
  - [Upload Objects into Bucket](#upload-objects-into-bucket)
  - [Share Objects Publicly](#share-objects-publicly)
  - [References](#references)

</details>

## Overview

Cloud Storage allows world-wide storage and retrieval of any amount of data at any time. You can use Cloud Storage for a range of scenarios including serving website content, storing data for archival and disaster recovery, or distributing large data objects to users via direct download. In this hands-on lab you will learn how to use the Cloud Console to create a storage bucket, then upload objects, create folders and subfolders, and make those objects publicly accessible.

## Create Buckets

1. In the Cloud Console, go to **Navigation Menu** > **Cloud Storage** > **Browser**.
2. Click **CREATE BUCKET**

There're the Bucket naming rules:

- Do not include sensitive information in the bucket name, because **the bucket namespace is global and publicly visible**.
- Bucket names must contain only lowercase letters, numbers, dashes (-), underscores (`_`), and dots (`.`). Names containing dots require [verification](https://cloud.google.com/storage/docs/domain-name-verification).
- Bucket names must start and end with a number or letter.
- Bucket names must contain 3 to 63 characters. Names containing dots can contain up to 222 characters, but each dot-separated component can be no longer than 63 characters.
- Bucket names cannot be represented as an IP address in dotted-decimal notation (for example, `192.168.5.4`).
- Bucket names cannot begin with the `"goog"` prefix.
- Bucket names cannot contain `"google"` or close misspellings of `"google"`.
- For DNS compliance and future compatibility, you should not use underscores (`_`) or have a period adjacent to another period or dash. For example, "`..`" or "`-.`" or "`.-`" are not valid in DNS names.


## Upload Objects into Bucket

There are two way to upload objects into the bucket in Google Console:

1. Drag your image to the **Just Add Data Area** of the Bucket details screen.
2. Click **Upload Files** and choose files in your local machine.

Notice the object names must be unique only within a given bucket.

## Share Objects Publicly

Follow steps below to create a publicly accessible URL for the object.

1. Click the **drop-down menu** (three vertical dots).
2. Select **Edit Permissions** from the drop-down menu.
3. In the dialog that appears, click the **+ Add entry** button.
4. Add permissions and then click **Save**.

## References

- [Cloud Storage Documentation](https://cloud.google.com/storage/docs)
- [Google Cloud Storage: Massive Scalability Plus More | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=081hh6EzlTk)