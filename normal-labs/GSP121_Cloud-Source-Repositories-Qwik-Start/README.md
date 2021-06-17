# GSP121 —— Cloud Source Repositories: Qwik Start

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Use Cloud Source Repository](#use-cloud-source-repository)
- [Browse Files in Cloud Source Repository](#browse-files-in-cloud-source-repository)
- [References](#references)

</details>

## Overview

[Google Cloud Source Repositories](https://cloud.google.com/source-repositories/) provides Git version control to support collaborative development of any application or service. In this lab, you will create a local Git repository that contains a sample file, add a Google Source Repository as a remote, and push the contents of the local repository. You will use the source browser included in Source Repositories to view your repository files from within the Cloud Console.

## Use Cloud Source Repository

```bash
# create repository
$ gcloud source repos create <REPO_NAME>

# clone contents from Cloud Source Repository
$ gcloud source repos clone REPO_DEMO
```

## Browse Files in Cloud Source Repository

1. Click **Navigation Menu** > **Source Repositories**.
2. Click **Source Code**

## References

- [Cloud Source Repository Documentation](https://cloud.google.com/source-repositories/docs)
- [`gcloud source repos create` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/source/repos/create)
- [`gcloud source repos clone` | Cloud SDK Documentation](https://cloud.google.com/sdk/gcloud/reference/source/repos/clone)