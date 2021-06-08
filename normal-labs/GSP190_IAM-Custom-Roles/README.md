# GSP190 —— IAM Custom Roles

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [GSP190 —— IAM Custom Roles](#gsp190--iam-custom-roles)
  - [Overview](#overview)
  - [IAM Custom Roles](#iam-custom-roles)
  - [Create a Custom Role](#create-a-custom-role)
  - [Update a Custom Role](#update-a-custom-role)
  - [Disable a Custom Role](#disable-a-custom-role)
  - [Delete a Custom Role](#delete-a-custom-role)

</details>

## Overview

## IAM Custom Roles

- Cloud IAM provides the ability to create customized Cloud IAM roles.
- We can create a custom Cloud IAM role and then grant that role to users.
- Represent form: `<service>.<resource>.<verb>`.
- Permissions usually, but not always, correspond 1:1 with REST methods.
- Custom roles can only be used to grant permissions in policies for the same project or organization that owns the roles or resources under them.

## Create a Custom Role

- To create a custom role, a caller must possess `iam.roles.create` permission.
- Use the `gcloud iam roles create` command to create new custom roles.
  - By providing a YAML file that contains the role definition
  - By using flags to specify the role definition.

```bash
$ gcloud iam roles create <role-id> \
    --project=<project-id> \
    --file=<yaml-file-path>
```

## Update a Custom Role

## Disable a Custom Role

## Delete a Custom Role