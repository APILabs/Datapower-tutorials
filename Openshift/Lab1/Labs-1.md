# Getting Started

**Prerequisites**:

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

    - Change directory to  datapower-tutorials/Openshift/Lab1

5. Retrieve the openshift token
    - Retrive the login and openshift token from the console. and paste the oc login command .

6. Login to openshift using cli
    - Once logged in, change to the openshift projecct : cp4i
        ```oc project cp4i```

    - The below resources do not have the namespace mentioned in the yamls, so when running the below commands be careful of the namespace.

7. Execute the commands to create the yaml files and create the resources.
    - Execute the below commands :
        - oc apply -f admin-secret.yaml
            This creates the secret for the admin password
        - oc apply -f web-mgmt-config.yaml
            This yaml consists of the below cfg file to enable the webui : 
                ```ssh
                web-mgmt
                admin-state enabled
                local-address 0.0.0.0
                port 9090
                save-config-overwrite
                idle-timeout 9000
                ssl-config-type server
                exit

                ```
        - oc apply datapower.yaml
            This yaml is the basic custom resource definition to create a datapower service
        - oc apply -f webui-service.yaml
            This service exposes the webui from the datapower container
        - oc apply -f webui-route.yaml
            This route exposes the webui from the datapower outside the openshift container
