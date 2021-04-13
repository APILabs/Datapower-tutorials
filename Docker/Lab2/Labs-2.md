# Getting Started

**Prerequisites**:
Access to a docker environment.
Check if there are no previous docker images running.
run docker ps or docker ps -a
If there are previous images

    ```
        docker stop <container_id>
        docker rm <container_id>
    ```

## Create your first  application on Datapower running on docker

1. git clone <https://github.com/APILabs/Datapower-tutorials.git>

2. Navigate to the folder Datapower-tutorials/Docker/Lab2

3. Lab2 uses the folder datapower-services/dp-demo to hold the custom application. Look through the file structure under dp-demo/drouter to see the files that will be mounted in the running container.

4. go to the utils folder Datapower-tutorials/Docker/Lab2/utils

5. Run the below command ./testLocalDatapower.sh
   This command run the datapower image and mounts the dp-demo folder directory into the container.
   If you want to make any changes to the files you can edit the files under
   /Docker/datapower-services/dp-demo/drouter

6. Test the service by calling
    If you are using the local sytem use -
    <https://localhost:6443/demo.html>

    If you are using Docker playground the sample url will be similar to below :

    <https://ip172-18-0-8-c1qj97re75e000ahroq0-6443.direct.labs.play-with-docker.com/demo.html>

7. You have now sucessfully tested the application deployed on datapower under domain IDP.

8. To make changes to local file . Navigate to the folder :

    cd ../datapower-services/dp-demo/drouter/local/IDP/
    Update the file - demo.html with any custom message

9. Refresh the service  url
    "<https://ip172-18-0-8-c1qj97re75e000ahroq0-6443.direct.labs.play-with-docker.com/demo.html"> to view the changes.
