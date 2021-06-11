# GSP064 —— Cloud IAM: Qwik Start

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Project Level Roles](#project-level-roles)

</details>

## Overview

Google Cloud's Identity and Access Management (IAM) service lets you create and manage permissions for Google Cloud resources. Cloud IAM unifies access control for Google Cloud services into a single system and provides a consistent set of operations.

## Project Level Roles

- **Primitive roles** set project-level permissions and unless otherwise specified, they control access and management to all Google Cloud services.
- The `Browser`, `Editor`, `Owner`, and `Viewer` are known as primitive roles in Google Cloud.

The following table pulls definitions from the [Google Cloud roles documentation](https://cloud.google.com/iam/docs/understanding-roles#primitive_roles), which gives a brief overview of `browser`, `viewer`, `editor`, and `owner` role permissions:

| Role Name | Permissions |
| :-- | :-- |
| `roles/viewer` | Permissions for read-only actions that do not affect state, such as viewing (but not modifying) existing resources or data. |
| `roles/editor` | All viewer permissions, plus permissions for actions that modify state, such as changing existing resources. |
| `roles/owner` | All editor permissions and permissions for the following actions: <br/><br/> 1. Manage roles and permissions for a project and all resources within the project. <br/> 2. Set up billing for a project. |
| `roles/browser` | Read access to browse the hierarchy for a project, including the folder, organization, and Cloud IAM policy. This role doesn't include permission to view resources in the project. |

## References

- [Manage Access Control with Google Cloud IAM | Google Cloud Labs | YouTube](https://www.youtube.com/watch?v=PqMGmRhKsnM)