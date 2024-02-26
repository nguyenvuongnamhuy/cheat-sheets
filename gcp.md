# Table of Contents

- [Login](#login)
- [Init](#init)
- [SSH](#ssh)
- [File transferring](#file-transferring)
- [Folder transferring](#folder-transferring)
- [Project](#project)
  - [List all projects](#list-all-projects)
  - [Switch project](#switch-project)
  - [Get current project](#get-current-project)
  - [List all instances](#list-all-instances-of-current-project)

# Login

```bash
gcloud auth login
gcloud auth application-default login
```

# Init

```bash
gcloud init
```

# SSH

```bash
gcloud compute ssh "${INSTANCE_NAME}" --project "${PROJECT_NAME}"
```

# File transferring

```bash
gcloud compute scp "${INSTANCE_NAME}":/path-to-instance-file /path-to-local-file --project "${PROJECT_NAME}"
```

# Folder transferring

```bash
gcloud compute scp --recurse "${INSTANCE_NAME}":/path-to-instance-folder /path-to-local-folder --project "${PROJECT_NAME}"
```

# Project

## List all projects

```bash
gcloud projects list
```

## Switch project

```bash
gcloud config set project ${PROJECT_ID}
```

## Get current project

```bash
gcloud config get-value project
```

## List all instances of current project

```bash
gcloud compute instances list
```

---
