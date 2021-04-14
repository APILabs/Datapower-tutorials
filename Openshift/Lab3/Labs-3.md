**Prerequisites**:

-Openshift/CP4I Environment

**Getting Started**:
This repository contain code and configuration files that could be used for an ArgoCD demonstration or for educations.

- argocd. It contains the files to deploy the ArgoCd instance.
- deploy: that has the datapower service and yaml files
- env_dev: It containt the deployment file used to deploy the sample in dev environment. In this case, a namespace named lab 3. The application.yaml file defines the application in ArgoCD. The kustomization.yaml adjust the deployment files for the specific dev environment (route customisation, namespace).
    This repository contains 3 samples

    The deployment of ArgoCD instance on OpenShift.
    The deployment of an application in dev and prod environments. Each environment has its own specificities (routes, namespace, config values ...).
    To deploy a datapower instance


**Deploy ArgoCD**

In the argocd directory, there are several yaml files that could be used to deploy an instance of ArgoCD.

This deployment uses the ArgoCD operator.

    1. Create the namespace, named argocd

    oc apply -f argocd/namespace.yaml

    2. Deploy the ArgoCD operator in the created namespace

    oc apply -f argocd/operator.yaml

    It creates an OperatorGroup, a subscriotpn to ArgoCD operator. It creates also a clusterroleinding to give priviliege to argocd to manage comopenents on the cluster.

    3. Create an instance of ArgoCD

    oc apply -f argocd/argocd_instance.yaml


The ArgoCD instance is basic but it include the definition of a route allowing toa ccess ArgoCD console and the integration with OpenShift authentication (dex).

**Deployment in dev environment**

In the env_dev directory, there are the files ensuring the deployment of the application. The application.yaml defines the ArgoCD appliacation and teh rule to monitor the synchronisation betwen the values in git and what it has been deployed on the cluster.

The kustomisation.yaml defines the specific deployment for dev environement. It is based on the common base defien d in the app_config dir of the git repo. The it add the specific namespaces. finally, it does some patch on default values to ensure the alignment with the dev environment. Here, it change the host of the route to be aligned with the specific namespace of the dev environment.

**To deploy the application in dev environment:**

oc apply -f env_dev/applications.yaml

on ArgoCD, yoi could the how the deployment is managed and what are the resourcees that are monitored to ensure the synchronisation with the confi inside the git reposistory.
