## Overview
The Manifests project is a Kubernetes configuration repository designed to be managed using [Kustomize](https://kustomize.io/) and deployed with [ArgoCD](https://argo-cd.readthedocs.io/). The project structure includes a set of Kubernetes manifests for configuring and deploying an application within a Kubernetes cluster.

Deployment to the Kubernetes cluster is handled automatically by ArgoCD, triggered by commits to the main branch of the repository.

## Project Structure
The project follows a well-structured layout consisting of two main components: **base** and **overlays**.

### Base Folder
The `base` folder contains the foundational Kubernetes manifests used to define the core resources of the application. Below is an overview of the key Kubernetes types present in the base folder:

- **Deployment**: Defines the pods and containerized services, including replica settings, image configuration, and environment variables for the application.
- **Service**: Exposes the application internally within the cluster or externally, providing access to the deployed pods via a defined networking layer.
- **ConfigMaps**: Stores configuration data for the application in key-value format, which can be injected into the pods at runtime.
- **Secrets**: Defines placeholder references for sensitive information, but no actual secrets or sensitive data are stored in this repository. All sensitive information is managed in the infra project at [https://gitlab.com/therealcisse/youtoo-infra](https://gitlab.com/therealcisse/youtoo-infra).

### Overlays Folder
The `overlays` folder is used to manage environment-specific configurations. Currently, the project only supports the `local` environment, which extends and customizes the `base` configuration to match the needs of a local development setup.

## Deployment Process
The deployment process for the application is managed by ArgoCD, which monitors the repository for changes. Once a commit is pushed to the main branch, ArgoCD automatically triggers the deployment of the updated manifests into the Kubernetes cluster. This automated deployment ensures that changes are continuously and consistently applied.

### Tooling
- **Kustomize**: The project uses Kustomize to create a layered configuration approach for Kubernetes manifests. Kustomize allows defining reusable and composable base configurations, while overlays can be used to customize them for different environments.
- **ArgoCD**: ArgoCD is responsible for the Continuous Deployment (CD) of the Kubernetes resources, ensuring that all changes are reflected in the cluster without manual intervention.

## Summary
The Manifests project utilizes Kustomize for managing Kubernetes configurations and ArgoCD for automating deployment. The core resources are defined in the `base` folder, while environment-specific customizations are held in the `overlays` folder. After changes are committed to the main branch, ArgoCD handles the deployment process to keep the Kubernetes cluster up-to-date.
