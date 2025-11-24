---
slug: github-create-deploy-cloud-run-job
title: Automating Google Cloud Run Job Deployment with Bash and Cloud Build
repo: justin-napolitano/create_deploy_cloud_run_job
githubUrl: https://github.com/justin-napolitano/create_deploy_cloud_run_job
generatedAt: '2025-11-23T08:47:04.580209Z'
source: github-auto
summary: >-
  A Bash script automates building, pushing, deploying, and executing Google Cloud Run jobs using
  Cloud Build and Container Registry.
tags:
  - google-cloud-run
  - cloud-build
  - bash
  - deployment-automation
  - docker
  - gcp
seoPrimaryKeyword: google cloud run job deployment
seoSecondaryKeywords:
  - bash automation
  - cloud build
  - docker image deployment
  - gcp automation
seoOptimized: true
---

# Technical Overview: Automating Cloud Run Job Deployment with Bash and Google Cloud Build

## Motivation

Deploying containerized workloads to Google Cloud Run as jobs involves multiple steps: building a Docker image, pushing it to a container registry, creating the Cloud Run job, and executing it. Manually performing these steps can be repetitive and error-prone, especially when iterating during development or deploying multiple jobs.

This project addresses the need for a streamlined, script-driven deployment process that encapsulates these steps into a single executable script. It reduces manual overhead and enforces consistency in deployment.

## Problem Statement

The manual deployment workflow for Cloud Run Jobs requires:

- Building a Docker image locally or via Cloud Build
- Pushing the image to Google Container Registry (GCR)
- Creating the Cloud Run job referencing the pushed image
- Executing the job

Each step involves specific commands and configuration files. Managing these steps manually can slow down development and introduce configuration drift.

## Implementation Details

The core of this repository is a Bash script (`create_deploy_cloud_run.sh`) that automates the entire deployment pipeline:

1. **Argument Parsing:** The script expects exactly three arguments: the Google Cloud project ID, the Docker image name, and the Cloud Run job name. It validates the input and exits with usage instructions if arguments are missing.

2. **Variable Setup:** It defines constants such as the deployment region (`us-west2`) and constructs the service account email based on the project ID.

3. **Dynamic `cloudbuild.yaml` Generation:** The script generates a `cloudbuild.yaml` file on the fly, which defines the build steps for Google Cloud Build:
   - Build the Docker image tagged as `gcr.io/$PROJECT_NAME/$IMAGE_NAME`.
   - Push the Docker image to Google Container Registry.
   - Create the Cloud Run job using the pushed image.

   The script includes commented-out sections for environment variable overrides related to service account authentication, allowing flexibility if needed.

4. **Build Submission:** Using `gcloud builds submit`, it submits the build to Google Cloud Build with the generated configuration.

5. **Job Execution:** After the job is created, the script immediately executes the Cloud Run job in the specified region.

6. **Feedback:** It outputs a success message upon completion.

## Assumptions and Considerations

- The script assumes the presence of a Dockerfile in the repository root to build the container image.
- It expects a service account key JSON file at `keys/service-account-key.json` for authentication, though the check is commented out to allow flexibility.
- The deployment region is hardcoded but can be parameterized in future iterations.
- Error handling is minimal; the script exits on incorrect usage but does not extensively validate cloud command success.

## Practical Usage

To use the script, a developer clones the repository, ensures their Python application and Dockerfile are present, makes the script executable, and runs it with the required arguments. This encapsulates the entire Cloud Run job deployment lifecycle in one command.

## Potential Improvements

- Parameterize deployment region and service account details.
- Add robust error handling and logging.
- Integrate environment variable and secret management.
- Provide example Python application and Dockerfile to facilitate onboarding.
- Support alternative container registries and multi-region deployments.

## Conclusion

This project offers a minimal yet effective automation tool for deploying Cloud Run Jobs on GCP. It leverages native Google Cloud tools and standard Bash scripting to reduce manual deployment steps, enabling faster iteration and consistent deployments. The approach is practical and extensible for more complex deployment pipelines.
