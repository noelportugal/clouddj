## Cloud Dj powered by Sonic Pi Introduction

In this guide, we'll show you a few simple steps to launch an Oracle Linux instance on Oracle Cloud Infrastructure, and then proceed to launch a Cloud Dj powered by [Sonic Pi](https://sonic-pi.net/) from your Cloud Linux instance. The path that we will take is as follows:

 - Launch your Oracle Linux instance in the Oracle cloud
 - Install Oracle Container Runtime for Docker
 - Install and run Cloud Dj

### Create an Oracle Linux instance on the Oracle Cloud Infrastructure
Follow [these instructions](oci.md) to create an Oracle Linux instance and the come back after you are done.

### Install and configure Docker
While connected to your Oracle Linux instance, run the following commands to install and configure the Docker container runtime.

```
sudo yum install docker-engine -y
sudo usermod -aG docker opc
sudo systemctl enable docker
sudo systemctl start docker
```

Before proceeding further, logout of the current SSH session, & then reconnect to your Oracle Linux instance and log back in vis SSH. _This is to ensure group membership configured in the previous step is correctly applied and in effect._
Once you have reconnected to the instance, run the following command to install the Fn CLI tool (this will download a shell script and execute it).

### Run Cloud Dj from Docker

	docker run --rm -p 8001:8001 -p 8002:8002 -p 4558:4558 sdaschner/sonicpi-clouddj:build-2

Notice we are specifying the ingress ports we configured on our Virtual Cloud Network.

Now you can access your Cloud Dj from the web at http://[virtual-server-public-instance]:8001/

#### Stop Cloud Dj from Docker
If you need to stop your docker instance you must logout from your shell session. Find the docker Id

	docker ps
	docker kill