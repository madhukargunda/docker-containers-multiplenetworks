# docker-containers-multiplenetworks
docker containers in multiple networks

In this article i am going to describe how to attach single container to multiple networks

## The Target Architecture

![docker-containers-on-multiple_networks](https://user-images.githubusercontent.com/5623861/56472489-8a9b9b80-6491-11e9-8d1c-3f02c3b25ab9.jpg)



Step 1 : Create three different docker images mysql,nginx and httpd using the below commands

```
  docker container run -d -p 3306:3306 --name mysqlmydb -e MYSQL_RANDOM_ROOT_PASSWORD=mysql mysql
  docker container run -d --name myproxy -p 80:80 nginx
  docker container run --name myhttpd -p 81:81 -d httpd
  
```
Step 2 : List the available docker networks

```
 By default when new container is created it will be attached to bridge network untill unless we specified 
 the network name while creating the container. 
 
 Execute the below command and find the bridge driver id
 
  docker network ls 

```
<img width="736" alt="docker_network_ls" src="https://user-images.githubusercontent.com/5623861/55671713-66529300-58c5-11e9-878b-bd075f8688a3.png">

```
Step 3 : Inspect the docker bridge driver using docker network 4f2

```
<img width="1642" alt="docker_bridge_network_inspect" src="https://user-images.githubusercontent.com/5623861/55671927-a286f300-58c7-11e9-8f99-aa435ac6761f.png">

```
Here three containers are attached to the brdige network by default

```
Step 4 : Create the custom network and assign all the containers to newly created network

```
docker network create --driver bridge myApplicationNetwork
docker network connect eff 755
docker network connect eff 60
docker network connect eff 38
```

Step5 : Inspect the newly created network 

<img width="1665" alt="docker network myappnetwork" src="https://user-images.githubusercontent.com/5623861/55671998-6607c700-58c8-11e9-83b5-3b354310ccab.png">

Step 6: Now all three containers are attached to the both the networks.
Refer the below screen image container is attached to the both the networks

```
Inspect the docker container and each container is attached to both the networks
docker container inspect 755
```
<img width="1633" alt="docker container inspect" src="https://user-images.githubusercontent.com/5623861/55672670-4379ac00-58d0-11e9-87b9-2338edcec7b4.png">


   


