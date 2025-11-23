# Cloud Run Job Deployment Script

This repository provides a Bash script to automate the building, deployment, and execution of a Cloud Run Job on Google Cloud Platform (GCP). It leverages Google Cloud Build to containerize a Python application and deploy it as a Cloud Run Job with minimal manual configuration.

## Features

- Automates Docker image build and push to Google Container Registry
- Dynamically generates a `cloudbuild.yaml` file for Google Cloud Build
- Creates and executes a Cloud Run Job in a specified region
- Uses a service account for authentication and permissions

## Tech Stack

- Shell scripting (Bash)
- Google Cloud SDK (`gcloud` CLI)
- Google Cloud Build
- Google Cloud Run
- Docker

## Getting Started

### Prerequisites

- Install and configure [Google Cloud SDK](https://cloud.google.com/sdk/docs/install)
- Install [Docker](https://docs.docker.com/get-docker/)
- Have a Google Cloud Project with billing enabled
- Create a service account with appropriate permissions and download its key JSON file to `keys/service-account-key.json`

### Installation

1. Clone the repository:

```bash
git clone https://github.com/justin-napolitano/create_deploy_cloud_run_job.git
cd create_deploy_cloud_run_job
```

2. Make the deployment script executable:

```bash
chmod +x create_deploy_cloud_run.sh
```

3. Ensure your Python application and `Dockerfile` are in the repository root.

### Usage

Run the deployment script with the following arguments:

```bash
./create_deploy_cloud_run.sh <PROJECT_NAME> <IMAGE_NAME> <JOB_NAME>
```

- `<PROJECT_NAME>`: Your Google Cloud project ID
- `<IMAGE_NAME>`: Desired Docker image name
- `<JOB_NAME>`: Name for the Cloud Run Job

Example:

```bash
./create_deploy_cloud_run.sh smart-axis-421517 my-python-job my-cloud-run-job
```

## Project Structure

```
create_deploy_cloud_run_job/
├── create_deploy_cloud_run.sh   # Main deployment script
├── Dockerfile                   # Dockerfile for Python application (assumed)
├── README.md                    # This README
├── index.md                    # Documentation/tutorial
└── keys/                       # Directory for service account key (not included)
```

- The script dynamically generates `cloudbuild.yaml` during execution.

## Future Work / Roadmap

- Add support for environment variables and secrets management
- Parameterize region and service account via CLI arguments
- Add validation and error handling for missing files and permissions
- Support for different programming languages beyond Python
- Integration tests for deployment pipeline
- Documentation enhancements with usage examples and troubleshooting
