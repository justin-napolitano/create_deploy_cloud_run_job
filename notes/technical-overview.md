---
slug: github-create-deploy-cloud-run-job-note-technical-overview
id: github-create-deploy-cloud-run-job-note-technical-overview
title: create_deploy_cloud_run_job Overview
repo: justin-napolitano/create_deploy_cloud_run_job
githubUrl: https://github.com/justin-napolitano/create_deploy_cloud_run_job
generatedAt: '2025-11-24T18:34:07.099Z'
source: github-auto
summary: >-
  This repo automates the deployment of a Cloud Run Job on Google Cloud Platform
  (GCP) via a Bash script. It builds and containerizes your Python app using
  Google Cloud Build, streamlining the whole process.
tags: []
seoPrimaryKeyword: ''
seoSecondaryKeywords: []
seoOptimized: false
topicFamily: null
topicFamilyConfidence: null
kind: note
entryLayout: note
showInProjects: false
showInNotes: true
showInWriting: false
showInLogs: false
---

This repo automates the deployment of a Cloud Run Job on Google Cloud Platform (GCP) via a Bash script. It builds and containerizes your Python app using Google Cloud Build, streamlining the whole process.

## Key Features

- Builds and pushes Docker images to Google Container Registry
- Dynamically generates a `cloudbuild.yaml` file
- Deploys and executes a Cloud Run Job in your specified region
- Uses a service account for authentication

## Quick Start

### Prerequisites

- Google Cloud SDK installed
- Docker installed
- Google Cloud Project with billing
- Service account key in `keys/service-account-key.json`

### Installation Steps

1. Clone the repo:

   ```bash
   git clone https://github.com/justin-napolitano/create_deploy_cloud_run_job.git
   cd create_deploy_cloud_run_job
   ```

2. Make the script executable:

   ```bash
   chmod +x create_deploy_cloud_run.sh
   ```

### Running the Script

Use this command:

```bash
./create_deploy_cloud_run.sh <PROJECT_NAME> <IMAGE_NAME> <JOB_NAME>
```

Example:

```bash
./create_deploy_cloud_run.sh smart-axis-421517 my-python-job my-cloud-run-job
```

**Gotcha:** Ensure the Dockerfile and Python app are in the root directory!
