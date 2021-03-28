# Getting Started

**Prerequisites**:
Complete Labs-1 and have a running datapower container.
Access to WebUI
Mounted Volumes

```docker
    -v $(pwd)/config:/opt/ibm/datapower/drouter/config \
    -v $(pwd)/local:/opt/ibm/datapower/drouter/local \
    -v $(pwd)/certs:/opt/ibm/datapower/root/secure/usrcerts \
```

## Create your first hello world application on Datapower

1. Git clone the repo

2. The repo has the below files :
domain config - poc.cfg
application zip file - test_service.zip
local files - helloworld_gatewayscript.js

3. Create a poc domain from the webui
    1. Create Domain poc
        - In the search field, enter domain.
        - From the search results, click Application Domain.
        - Click Add or New.
        - Define the basic properties: Name, administrative state, and descriptive summary.
        - Click Apply.

4. Create the application on the docker environment.
    1. From the Webui
        - Chose the new domain created from the drop down.
        - Import the test application(test_service.zip)
        - Inspect the test service and confirm that the service is running from the port numbers exposed on the container run command(8000 - 8010)
    2. From the cli
        - Navigate to the folder that contains to config, local and certs folders
        - Copy poc.cfg file to the config folder.
            Example: /root/Datapower/config/poc
        - Copy the local files to the local folder.
            Example : root/Datapower/local/poc
        - Refresh the browser and check if the test application(MPG) is available on the poc domain.
5. Test the application to recieve a hello world message.
