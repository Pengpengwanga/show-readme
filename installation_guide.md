# Installation and Configuration Guide
Flowgate can be installed by one of two approaches: 

- **Source installer:** The installer downloads Flowgate's source code from github. Please refer to **[Flowgate Compile Guide](compile_guide.md)**.

- **Binary installer:** The installer downloads Flowgate's Binary from server https://url. 


This guide describes the steps to install and configure Flowgate by using the Source or Binary installer. The run processes are almost the same. 

## Prerequisites for the target host
Flowgate is deployed as several Docker containers, and can be deployed on any Linux distribution that supports Docker. The target host requires Git, Docker, and Docker Compose to be installed.  
### Hardware
|Resource|Capacity|Description|
|---|---|---|
|CPU|minimal 2 CPU|4 CPU is preferred|
|Mem|minimal 4GB|8GB is preferred|
|Disk|minimal 40GB|160GB is preferred|
### Software
|Software|Version|Description|
|---|---|---|
|Docker engine|version 1.10 or higher|For installation instructions, please refer to: https://docs.docker.com/engine/installation/|
|Docker Compose|version 1.6.0 or higher|For installation instructions, please refer to: https://docs.docker.com/compose/install/|
|Git|latest is preferred|For installation instructions, please refer to: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git|
### Network ports 
|Port|Protocol|Description|
|---|---|---|
|443|HTTPS|Flowgate portal and core API will accept requests on this port for https protocol|
|80|HTTP|Flowgate portal and core API will accept requests on this port for http protocol|

## Installation Steps


### Source Installation
Please refer to **[Flowgate Compile Guide](compile_guide.md)**.

### Binary Installation

1. Download the installer from server https://url;
2. Use *tar* command to extract the package.
```
    $ sudo tar xvf flowgate-*.tar
```

3. Then you will get three files, ```flowgate_run.sh```, ```conf.tar.gz```, ```flowgate.tar```.Put them into the same folder and loading docker images:
```
    $ sudo docker load < flowgate.tar
```

## Finishing installation and starting Flowgate

### Start Flowgate

```
    $ sudo bash flowgate_run.sh
```
*Note*
1. Source Installation flowgate_run.sh file under *flowgate/make* folder.
2. Binary Installation flowgate_run.sh file extract from flowgate-*.tar.

If everything worked properly, you should be able to open a browser to visit the admin portal at **https://yourdomain** (change *yourdomain* to your server's hostname). Note that the default administrator username/password are admin/Admin!23.

### Managing Flowgate's lifecycle
You can use docker-compose to manage the lifecycle of Flowgate. Some useful commands are listed as follows (must run in the same directory as *docker-compose.run.images.yml*).

Stopping Flowgate:
```
$ sudo docker-compose -f docker-compose.run.images.yml down
Stopping flowgate-labsdb-worker-container ... done
Stopping flowgate-nlyte-worker-container ... done
Stopping flowgate-vc-worker-container ... done
Stopping flowgate-poweriq-worker-container ... done
Stopping flowgate-management-container ... done
Stopping flowgate-infoblox-worker-container ... done
Stopping flowgate-vro-worker-container ... done
Stopping flowgate-aggregator-container ... done
Stopping flowgate-api-container ... done
Stopping flowgate-redis-container ... done
Stopping flowgate-mongo-container ... done
Removing flowgate-labsdb-worker-container ... done
Removing flowgate-nlyte-worker-container ... done
Removing flowgate-vc-worker-container ... done
Removing flowgate-poweriq-worker-container ... done
Removing flowgate-management-container ... done
Removing flowgate-infoblox-worker-container ... done
Removing flowgate-vro-worker-container ... done
Removing flowgate-aggregator-container ... done
Removing flowgate-api-container ... done
Removing flowgate-redis-container ... done
Removing flowgate-mongo-container ... done
Removing network mavendockerbuild_db-network
Removing network mavendockerbuild_services-network
```  
Restarting Flowgate after stopping:
```
$ sudo docker-compose -f docker-compose.run.images.yml up -d
Creating network "mavendockerbuild_db-network" with the default driver
Creating network "mavendockerbuild_services-network" with the default driver
Creating flowgate-mongo-container
Creating flowgate-redis-container
Creating flowgate-api-container
Creating flowgate-aggregator-container
Creating flowgate-nlyte-worker-container
Creating flowgate-labsdb-worker-container
Creating flowgate-management-container
Creating flowgate-vc-worker-container
Creating flowgate-infoblox-worker-container
Creating flowgate-vro-worker-container
Creating flowgate-poweriq-worker-container
```  

## Troubleshooting
1. When Flowgate does not work properly, run the below commands to find out if all containers of Flowgate are in **UP** status: 
```
    $ sudo docker-compose -f docker-compose.run.images.yml ps
               Name                             Command               State                    Ports                  
---------------------------------------------------------------------------------------------------------------------
flowgate-aggregator-container        sh start.sh                      Up                                              
flowgate-api-container               sh start.sh                      Up      49610/tcp                               
flowgate-infoblox-worker-container   sh start.sh                      Up                                              
flowgate-labsdb-worker-container     sh start.sh                      Up                                              
flowgate-management-container        sh start.sh                      Up      443/tcp, 0.0.0.0:443->49611/tcp, 80/tcp 
flowgate-mongo-container             docker-entrypoint.sh mongod      Up      27017/tcp                               
flowgate-nlyte-worker-container      sh start.sh                      Up                                              
flowgate-poweriq-worker-container    sh start.sh                      Up                                              
flowgate-redis-container             docker-entrypoint.sh redis ...   Up      6379/tcp                                
flowgate-vc-worker-container         sh start.sh                      Up                                              
flowgate-vro-worker-container        sh start.sh                      Up  
```
If a container is not in **UP** state, check the log file of that container in directory ```/opt/vmware/flowgate/log```. For example, if the container ```flowgate-api-container``` is not running, you should look at the log file ```/opt/vmware/flowgate/log/flowgate-api/*.log```.  
