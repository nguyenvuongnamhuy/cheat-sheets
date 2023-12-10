# Table of Contents

- [GCP](#gcp-commands)
  - [Login](#login)
  - [SSH](#ssh)
  - [File transferring](#file-transferring)
  - [Folder transferring](#folder-transferring)

# GCP commands

## Login

```bash
gcloud auth login
```

## SSH

```bash
gcloud compute ssh "${INSTANCE_NAME}" --project "${PROJECT_NAME}"
```

## File transferring

```bash
gcloud compute scp "${INSTANCE_NAME}":/path-to-instance-file /path-to-local-file --project "${PROJECT_NAME}"
```

## Folder transferring

```bash
gcloud compute scp --recurse "${INSTANCE_NAME}":/path-to-instance-folder /path-to-local-folder --project "${PROJECT_NAME}"
```

---
