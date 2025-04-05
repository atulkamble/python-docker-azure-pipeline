# Docker Image Build Pipeline

This repository contains an Azure DevOps pipeline configuration that automates the process of building a Docker image whenever changes are pushed to the `main` branch.

## Overview

The pipeline performs the following tasks:

- Triggers on changes to the `main` branch
- Builds a Docker image using the specified Dockerfile
- Tags the image using the Azure DevOps build ID

## Pipeline Configuration

The pipeline is defined in an Azure Pipelines YAML file. Below is a summary of its configuration:

- **Trigger:** The pipeline runs on every commit to the `main` branch.
- **Resources:** Uses the self repository as the source.
- **Variables:**
  - `tag`: Uses the `Build.BuildId` to tag the Docker image.
- **Stages:**
  - **Build Stage:** Uses the latest Ubuntu image to run the build.
    - **Steps:**
      - Runs the `Docker@2` task to build the Docker image from a `Dockerfile` located anywhere in the repository.

## Docker Task Details

- **Task:** `Docker@2`
- **Command:** `build`
- **Dockerfile:** Automatically discovers any `Dockerfile` in the repository using the `**/Dockerfile` glob pattern.
- **Tags:** Applies the Azure DevOps build ID as the Docker image tag.

## References

For more information, see the [official Microsoft documentation on Docker tasks in Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/languages/docker).
