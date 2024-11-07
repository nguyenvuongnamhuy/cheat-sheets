# Table of Contents

- [Login](#login)
- [Init](#init)
- [SSH](#ssh)
- [File transferring](#file-transferring)
- [Folder transferring](#folder-transferring)
- [Account](#account)
  - [List all](#list-all-activate-account)
  - [Create account](#create-account)
  - [Switch account](#switch-another-account-with-current-config)
  - [Configuration](#configuration)
    - [List all](#list-all-configs)
    - [Create config](#create-config)
    - [Switch config](#switch-another-config-with-current-account)
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

# Account

## List all activate account

```bash
gcloud auth list
```

## Create account

Login to create account

## Switch another account with current config

```bash
gcloud config set account user1@example.com
```

## Configuration

### List all configs

```bash
gcloud config configurations list
```

### Create config

should be username in email

```bash
gcloud config configurations create ${USERNAME}
gcloud config set account ${EMAIL}
gcloud config set project ${PROJECT_ID}
```

### Switch another config with current account

```bash
gcloud config configurations activate ${USERNAME}
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
