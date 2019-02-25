# SparkMLApplication (Project in Progress)
We will build a SparkML application to build sentiment analysis model for Nike using Twitter Data.
We will then visualize various metrics using Hive mapping to HBase table.

# Setup
## Setup HDP Sandbox

1. Install Docker toolbox and run as Administrator

Prerequisites:
1. HDP Sandbox requires minimum 10GB allocated to the virtual machine
2. Allocate maximum size to disk space to pull large images

Docker commands:
```
$ docker-machine rm default
$ docker-machine create -d virtualbox --virtualbox-disk-size "100000" --virtualbox-memory "10240" default
```

<!-- ## Troubleshooting
1. Docker toolbox required the working directory to be shareable to be able to mount the proxy sandbox folders to the container.\
To mount contents of a folder to the container, follow the folowing steps:\
Navigate to ~/.docker/machine/machines/default/default \
Edit the VBOX-PREV file with the following additon
```
<SharedFolders>
        <SharedFolder name="c/Users" hostPath="\\?\c:\Users" writable="true" autoMount="true"/>
        -- New addition
        <SharedFolder name="WorkDir" hostPath="\\?\<insert your path here>"
                      writable="true" autoMount="true"/>
      </SharedFolders>
```
2.  Error response from daemon: cgroups: cannot find cgroup mount destination: unknown. \
Solution
```
$ docker-machine ssh default "sudo mkdir /sys/fs/cgroup/systemd"
$ docker-machine ssh default "sudo mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd"
```
-->
## HDP Deployment

Download deployment scripts for Docker from [here](https://hortonworks.com/downloads/#sandbox)
1. For simplest installation, make sure that you download and extract the scripts in your Download folder  
2. Run Git Bash in your extracted folder and execute the deployment script  docker-deploy-hdp<version>  
        ```
        $ sh docker-deploy-hdp30
        ```  

**Troubleshooting for proxy deploy**  
1. If you get docker error for invalid reference format, replace your system path in proxy-deploy.sh script with $(pwd) to map volumes  For example:  
In my [script](https://github.com/swatisingh0107/SparkMLApplication/blob/master/HDP3.0.1/sandbox/proxy/proxy-deploy.sh), I've replaced \C:\Users\swati\Downloads\HDP3.0.1 with \\$PWD    
Rexecute proxy-deploy in Git Bash  

2.  Error response from daemon: cgroups: cannot find cgroup mount destination: unknown. \
Solution \
```
$ docker-machine ssh default "sudo mkdir /sys/fs/cgroup/systemd"
$ docker-machine ssh default "sudo mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd"
$ sandbox/proxy/proxy-deploy.sh
``` 

3. If you want to run Connected Data Architectures, i.e. executing Hortonworks various services on a single node, both HDP and HDF should have CDA enabled. This statement is true for HDP 2.6.5 and HDF 3.1.1. CDA Sandbox is disabled for HDP 3.0.1 until further notice. To ensure, you have correct version of the image, check docker-deploy script and update the version. \

## Map Sandbox to Host
1. Run cmd as administrator  
2. Navigate to c:\Windows\System32\drivers\etc\hosts  
3. Type 'dir' to check if you are in correct directory  
4. Type 'attrib' to check if hosts file is available for edit. The hosts file will have -r if it is readonly. To remove read-only permission use 'attrib -r hosts'  
5. Now type 'notepad hosts' to open the hosts file in notepad.  
6. Add {IP-Address} localhost sandbox-hdp.hortonworks.com sandbox-hdf.hortonworks.com   
7. Save the file  

**IMPORTANT**: Replace {IP-Address} with Sandbox IP Address.  

To check Sandbox IP address, in docker, execute ```$ docker-machine config <machine-name>```

# Application

1. [What is sentiment analysis?](https://github.com/swatisingh0107/SparkMLApplication/blob/master/Sentiment%20Analysis/Readme.md)
