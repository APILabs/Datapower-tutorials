# Getting Started

**Prerequisites**:

1. Completing Lab 1 and have an existing datapower instance running.

**Steps**:

-Openshift/CP4I Environment

1. Set up Environment
    use ibm demos url
    Link <https://www.ibm.com/cloud/garage/dte/tutorial/connect-app-integration-message-queue-using-cloud-pak-integration-using-openshift-42>

2. Start the environment:

    - Follow the Task1 steps mentioned on the demo url to start the environment and login to the environment
    - Log in to the Linux desktop with userid: ibmuser and password: engageibm.

    - Once on the linux desktop login to the openshift console using FireFox. Use htpasswd option. The user details are already saved and should allow you to access the console.

3. Login to openshift
    - Go to the openshift project cp4i. In an ideal environment, the operators will be installed across all namespaces and it would be better to have a seperate namespace for datapower. As this is a demo cluster, the operators are only installed on the cp4i namespace. Due to this all deployments and changes wil be done only on the cp4i cluster.

4. Clone the repository
    - Open the terminal application on the linux desktop and clone the repository.
         ```git clone <https://github.com/APILabs/Datapower-tutorials.git>```

    - Change directory to  Datapower-tutorials/Openshift/Lab2/deploy

5. Retrieve the openshift token
    - Retrive the login and openshift token from the console. and paste the oc login command .

6. Login to openshift using cli
    - Once logged in, change to the openshift projecct : cp4i
        ```oc project cp4i```

    - The below resources do not have the namespace mentioned in the yamls, so when running the below commands be careful of the namespace.

7. The config maps and secrets are to be created for the below :
    - IDP domain config
    - IDP domain local
    - IDP Domain certs
    
    To create the config map of the config
    ``` ```

        To create the config map of the local
    ``` ```

        To create the config map of the certs
    ```oc create secret generic idp-crypto-secret --from-file=Datapower-tutorials/Openshift/Lab2/ --from-file=Datapower-tutorials/Openshift/Lab2/```

    Execute the commands to create the yaml files and create the resources.
    - Execute the below commands :
        - oc apply -f datapower.yaml
            This yaml is the custom resource definition to create a datapower service along with the configuration of the IDP service and certificates
        - oc apply demo-service.yaml
            This service exposes the demo service port from the datapower container
        - oc apply demo-route.yaml
            This route exposes the demo service endpoint from the datapower outside the openshift container
