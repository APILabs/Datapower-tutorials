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

    - Go to the openshift project cp4i. In an ideal environment, the operators will be installed across all namespaces and it would be better to have a seperate namespace for datapower. As this is a demo cluster, the operators are only installed on the cp4i namespace. Due to this all deployments and changes wil be done only on the cp4i cluster.

    - Open the terminal application on the linux desktop and clone the repository.
         ```git clone <https://github.com/APILabs/Datapower-tutorials.git>```

    - Change directory to  datapower-tutorials/openshift/Lab1

    - Retrive the login and openshift token : 

    - Change to the openshift projecct : cp4i 
        ```oc project cp4i```

    - oc apply admin-secret.yaml

    - oc apply web-mgmt-config.yaml

    - oc apply datapower.yaml

    - oc apply webui-service.yaml

    - oc apply webui-route.yaml
