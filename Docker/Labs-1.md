# Getting Started

![demo](start-with-docker.gif)

**Prerequisites**: 

-Docker
-If you dont have a docker environment, you can use any of the docker environments on katacoda to run these steps.

Example run time environments for docker :
-https://labs.play-with-docker.com
-

**Duration**: 7 minutes

This tutorial will demonstrate how you can quickly setup gateway services to secure and optimize access to backend services.


# Development Environment

DataPower Gateways do not require a formal development environment. The majority of the configuration is performed using the Web GUI. If you need to write development artifacts, such as JavaScript or XSLT, then you can use any text editor and use Docker volume mounts to make them available to the DataPower container file system. It's the same if you want to change the configuration -- whenever you save your changes, DataPower writes files. When those files are in directories that are both Docker volumes and in version control, you win! No need to copy files around or do special builds just to try out your changes.

It's the same if you are starting with a project someone else has started. Just pull in the directories with the configuration and profit!

# Get your DataPower engine started

We love things that simply work with minimal effort. Deploying your first DataPower Gateway should be a similar experience to driving a brand new car (without the new car smell). The following steps should get you on the highway!

1. Open the docker command prompt and create a new directory called **datapower**. You will run your DataPower container from this directory `cd datapower`
2. Pull down the DataPower docker image from DockerHub. Of course this is optional, Docker is smart enough to get the image when it is run. Still, this might be a good time to familiarize yourself with what the image provides. See the [ibmcom/datapower](https://hub.docker.com/r/ibmcom/datapower/) Docker Hub page for details.

    ```
    docker pull ibmcom/datapower:latest
    ```

3. After the download completes, the DataPower image should appear in your registry

    ```
    REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
    ibmcom/datapower         latest              62ce04e36704        4 days ago          852.3 MB
    ```
4. Create a Datapower Directory
    ```
    mkdir Datapower
    cd Datapower
    ```
4. Start the container for the first time with the command below:
    Ensure that you are in the Datapower folder.

-Without Mounted Volume Directories 
```

    docker run -it -e DATAPOWER_ACCEPT_LICENSE=true -e  DATAPOWER_INTERACTIVE=true -p 9090:9090 ibmcom/datapower:latest
```
-With Mounted Volume Directories

You can create 3 subdirectories  - 
mkdir config local certs


```
$Datapower: 
docker run -it --name datapower \
-v $(pwd)/config:/opt/ibm/datapower/drouter/config \
-v $(pwd)/local:/opt/ibm/datapower/drouter/local \
-v $(pwd)/certs:/opt/ibm/datapower/root/secure/usrcerts \
-e DATAPOWER_ACCEPT_LICENSE="true" \
-e DATAPOWER_INTERACTIVE="true" \
-p 9090:9090 -p 9022:22 -p 5554:5554 -p 5550:5550 -p 8000-8010:8000-8010 \
ibmcom/datapower:latest 
```

    **Note:** 
    * **Ports:** Expose ports on the host system using (_-p nn:nn_) or let Docker choose the ports (_-p nn_). If you're running multiple containers on the same host system, you should let Docker choose the ports for you.
    * **/drouter/config** is the location where DataPower will persist the configuration using an easy to read and editable format.
    * **/drouter/local** is used to store source files such as JavaScript (GatewayScript), XSLT, key, certificates and so on.
    * **DATAPOWER_INTERACTIVE=true** prompts for login to the DataPower CLI on stdin and must be used with -it. This intermixes log output, disable DATAPOWER_LOG_STDOUT if not desired.

5. Login to the CLI 

```
docker attach <container_id> to enter the docker terminla. To complete the initial setup, default username is `admin` and also password is `admin`
6. Enable the Web GUI - this will be your primary development interface
    ```
    # configure terminal
    # web-mgmt
    # admin-state "enabled"
    # exit  
    ```
7. Hooray! You have completed the initial setup. If u are using your own system to run this lab , you can use https://localhost:9090 to login to the webui. If using the docker lab environment then 
1. Click on "open port and enter 9090". This will open a http url be default. update the url to https and you should be able to see the webui screen.

**Note**: If your docker machine is not running on localhost, enter the command `docker-machine ip` to find the host ip address.  
8. Make a note of the directories created when you run the container. These directories are mounted from the container file system to your local file system. Any edits from your workstation are picked up immediately.
```
$ ls
config	local 
```

# Summary

In this section, you pulled down the latest DataPower Docker image and started the DataPower container. You performed some basic configuration to enable the Web GUI.

**Next Step**: [Experience the CLI and WebUI](experience-cli-webgui.md)