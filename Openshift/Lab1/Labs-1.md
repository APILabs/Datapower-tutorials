# Getting Started

**Prerequisites**:

-Openshift/CP4I Environment
-If this is only for a poc you could also use the katacoda/kode cloud

- use ibm demos url 
 Link <https://www.ibm.com/cloud/garage/dte/tutorial/connect-app-integration-message-queue-using-cloud-pak-integration-using-openshift-42>

- Follow the Task1 steps mentioned on the demo url to start the environment and login to the environment
  Log in to the Linux® desktop with userid: ibmuser and password: engageibm.

- Once on the linux desktop login to the openshift console using FireFox. Use htpasswd option. The user details are already saved and should allow you to access the console.

- go to the openshift project cp4i
- git clone <https://github.com/APILabs/Datapower-tutorials.git>

- move the directory openshift/Lab1

- login to openshift

- oc project cp4i

- oc apply admin-secret.yaml

- oc apply web-mgmt-config.yaml

- oc apply datapower.yaml

- oc apply webui-service.yaml

- oc apply webui-route.yaml



