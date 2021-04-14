This repository contain code and configuration files that could be used for an ArgoCD demonstration or for educations.

- argocd. It contains the files to deploy the ArgoCd instance.
- deploy: that has the datapower service and yaml files
- env_dev: It containt the deployment file used to deploy the sample in dev environment. In this case, a namespace named lab 3. The application.yaml file defines the application in ArgoCD. The kustomization.yaml adjust the deployment files for the specific dev environment (route customisation, namespace).
    This repository contains 3 samples

    The deployment of ArgoCD instance on OpenShift.
    The deployment of an application in dev and prod environments. Each environment has its own specificities (routes, namespace, config values ...).
    To deploy a datapower instance