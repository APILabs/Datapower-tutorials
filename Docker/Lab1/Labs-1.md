# Getting Started

**Prerequisites**:

-Docker
-If you dont have a docker environment, you can use any of the docker environments on katacoda to run these steps.
-Example run time environments for docker- <https://labs.play-with-docker.com>

**Duration**: 7 minutes

This tutorial will demonstrate how you can quickly setup gateway services to secure and optimize access to backend services.

## Development Environment

DataPower Gateways do not require a formal development environment. The majority of the configuration is performed using the Web GUI. If you need to write development artifacts, such as JavaScript or XSLT, then you can use any text editor and use Docker volume mounts to make them available to the DataPower container file system. It's the same if you want to change the configuration -- whenever you save your changes, DataPower writes files. When those files are in directories that are both Docker volumes and in version control, you win! No need to copy files around or do special builds just to try out your changes.

It's the same if you are starting with a project someone else has started. Just pull in the directories with the configuration and profit!

## Get your DataPower engine started

We love things that simply work with minimal effort. Deploying your first DataPower Gateway should be a similar experience to driving a brand new car (without the new car smell). The following steps should get you on the highway!

1. Open the docker command prompt and create a new directory called **datapower**. You will run your DataPower container from this directory

    ```bash
    mkdir Datapower
    cd Datapower
    ```

2. Pull down the DataPower docker image from DockerHub. Of course this is optional, Docker is smart enough to get the image when it is run. Still, this might be a good time to familiarize yourself with what the image provides. See the [ibmcom/datapower](https://hub.docker.com/r/ibmcom/datapower/) Docker Hub page for details.

    ```docker
    docker pull ibmcom/datapower:latest
    ```

3. After the download completes, the DataPower image should appear in your registry

    ```docker
    REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
    ibmcom/datapower         latest              62ce04e36704        4 days ago          852.3 MB
    ```

4. Start the container for the first time with the command below:
    Ensure that you are in the Datapower folder. The 2 options that are can run the datapower environment.
    The below docker command opens ports
    9090 - Webui
    9022 - ssh
    5554/5550 - rest and xml management interfaces
    8000-8010 - any services that you create you can use this port range.

    -Without Mounted Volume Directories

    ```docker
    docker run -it -d -e DATAPOWER_ACCEPT_LICENSE=true -e  DATAPOWER_INTERACTIVE=true -p 9022:22 -p 5554:5554 -p 5550:5550 -p 8000-8010:8000-8010 -p 9090:9090 ibmcom/datapower:latest
    ```

    -With Mounted Volume Directories

    You can create 3 subdirectories  -
    mkdir config local certs.
     Give full permission to the folders
    chmod 777 *

    From the datapower directory

    ```docker
    docker run -it -d --name datapower \
    -v $(pwd)/config:/opt/ibm/datapower/drouter/config \
    -v $(pwd)/local:/opt/ibm/datapower/drouter/local \
    -v $(pwd)/certs:/opt/ibm/datapower/root/secure/usrcerts \
    -e DATAPOWER_ACCEPT_LICENSE="true" \
    -e DATAPOWER_INTERACTIVE="true" \
    -p 9090:9090 -p 9022:22 -p 5554:5554 -p 5550:5550 -p 8000-8010:8000-8010 \
    ibmcom/datapower:latest
    ```

    **Note**

    * **Ports:** Expose ports on the host system using (_-p nn:nn_) or let Docker choose the ports (_-p nn_). If you're running multiple containers on the same host system, you should let Docker choose the ports for you.
    * **/drouter/config** is the location where DataPower will persist the configuration using an easy to read and editable format.
    * **/drouter/local** is used to store source files such as JavaScript (GatewayScript), XSLT, key, certificates and so on.
    * **DATAPOWER_INTERACTIVE=true** prompts for login to the DataPower CLI on stdin and must be used with -it. This intermixes log output, disable DATAPOWER_LOG_STDOUT if not desired.

5. Login to the CLI

    ```docker
    docker ps

    Example : 2470794a83a1   ibmcom/datapower:latest   "/opt/ibm/datapower/…"   7 seconds ago   Up 5 seconds   0.0.0.0:5550->5550/tcp, 0.0.0.0:5554->5554/tcp, 0.0.0.0:8000-8010->8000-8010/tcp, 0.0.0.0:9090->9090/tcp, 0.0.0.0:9022->22/tcp   priceless_turing


    docker attach <container_id> to enter the docker terminal. In the above example container_id - "2470794a83a1"
    Then press enter and you will see the "login prompt"

    ```

    To complete the initial setup, default username is `admin` and also password is `admin`

6. Enable the Web GUI - this will be your primary development interface

    ```script
    # co
    # web-mgmt
    # admin-state "enabled"
    # exit  
    idg(config)# 20210413T062049.855Z [0x8100003f][mgmt][notice] domain(default): tid(319): Domain configuration has been modified.
    20210413T062049.893Z [0x00350014][mgmt][notice] web-mgmt(WebGUI-Settings): tid(303): Operational state up
    ```

   To exit from the container press Ctrl p+q and exit without killing the container. To ensure the container is still running run
   docker ps

   If no entries are found you can use docker ps -a to check stopped containers.
   docker start <container_id> to start any stopped containers.

7. Hooray! You have completed the initial setup. If u are using your own system to run this lab , you can use <https://localhost:9090> to login to the webui.
If using the docker lab environment(labs.play-with-docker.com) then Click on "open port and enter 9090". This will open a http url be default. Update the url to https and you should be able to see the webui screen.

**Note**: If your docker machine is not running on localhost, enter the command `docker-machine ip` to find the host ip address.  
8. If you have run the container using the mounted volumes , make a note of the directories created when you run the container. These directories are mounted from the container file system to your local file system. Any edits from your workstation are picked up immediately.

Try the below on datapower and check the file system on the local system
    - create a new domain
    - upload a file in the file management

```bash
$ ls
config local
```

## Summary

In this section, you pulled down the latest DataPower Docker image and started the DataPower container. You performed some basic configuration to enable the Web GUI.
