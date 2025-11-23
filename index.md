---
slug: "github-create-deploy-cloud-run-job"
title: "create_deploy_cloud_run_job"
repo: "justin-napolitano/create_deploy_cloud_run_job"
githubUrl: "https://github.com/justin-napolitano/create_deploy_cloud_run_job"
generatedAt: "2025-11-23T08:31:16.302758Z"
source: "github-auto"
---


# Technical Overview: Automated Deployment of Cloud Run Jobs via Shell Script

This project addresses the need for a streamlined, repeatable process to build and deploy Cloud Run Jobs on Google Cloud Platform (GCP) using a Bash script. The core challenge is automating container image creation, pushing it to Google Container Registry, and deploying it as a Cloud Run Job with minimal manual intervention.

## Motivation

Deploying Cloud Run Jobs typically involves multiple manual steps: building a Docker image, pushing it to a container registry, creating the job, and then executing it. This process can be error-prone and repetitive, especially when iterated frequently during development or CI/CD workflows. The script encapsulates these steps into a single command, reducing friction and potential for error.

## Problem Solved

- Manual Docker image build and push steps are automated.
- Cloud Build configuration (`cloudbuild.yaml`) is dynamically generated, avoiding the need to maintain a separate static file.
- Creation and execution of Cloud Run Jobs are integrated into the build pipeline.
- The script enforces argument validation and uses a consistent service account for permissions.

## How It's Built

The repository contains a single primary Bash script, `create_deploy_cloud_run.sh`. The script expects exactly three arguments: GCP project name, Docker image name, and Cloud Run Job name.

### Script Workflow

1. **Argument Validation:** Ensures exactly three arguments are provided.
2. **Variable Initialization:** Sets project name, image name, job name, region (hardcoded to `us-west2`), and service account email.
3. **Dynamic `cloudbuild.yaml` Generation:**
   - Defines build steps:
     - Build Docker image tagged as `gcr.io/$PROJECT_NAME/$IMAGE_NAME`.
     - Push the image to Google Container Registry.
     - Create the Cloud Run Job referencing the pushed image.
   - The build timeout is set to 1200 seconds.
4. **Build Submission:** Uses `gcloud builds submit` with the generated config.
5. **Job Execution:** Runs the Cloud Run Job immediately after creation.

### Assumptions and Notes

- The script assumes a `Dockerfile` is present in the current directory.
- The service account key JSON file is expected at `keys/service-account-key.json`, but the script comments out the check for its presence, implying optional manual enforcement.
- The region is fixed and not configurable via script arguments.
- Environment variables for authentication override in Cloud Build are commented out but available for use if needed.

## Practical Considerations

- The script is designed for simplicity and quick deployment but lacks robust error handling and configurability.
- It is suitable for developers familiar with GCP and Cloud Run who want to automate deployment without setting up full CI/CD pipelines.
- The dynamic generation of `cloudbuild.yaml` ensures the build steps are always in sync with the script logic, reducing maintenance overhead.

## Potential Extensions

- Parameterizing region and service account to support multiple environments.
- Adding support for environment variables, secrets, and other Cloud Run Job configurations.
- Integrating with CI/CD systems for automated triggers.
- Adding validation for required files and permissions before proceeding.

This project serves as a practical reference for automating Cloud Run Job deployments using Google Cloud Build and shell scripting, balancing simplicity with essential automation capabilities.