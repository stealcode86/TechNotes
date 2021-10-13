# TechNotes

Important links 
https://www.cncf.io/

https://hub.docker.com/ [ You need to sign up and get a dockerID ] 

Docker fundamentals 
https://lex.infosysapps.com/en/app/toc/lex_12740935231076542000/overview
hands on : 
https://labs.play-with-docker.com/
https://training.play-with-docker.com/
https://comparecloud.in/

Bare metal -> VM -> Containers -> Serverless 

context  - single bag 
A -> B 
Appln(place) -> place(Appln) 
Portable 
Appln + dependent libraries 

Mobile handset -> HW, OS , system apps , user installed apps 

***************
Installation - Skip (Lab play/ Training play URL ) 
**************
Types of containers 
Interactive 
Daemonized 

Program -  set of instructions 
PRocess  - when program is in execution 

=======================================================



    
4.    VOLUMES
 
Data volumes are designed to persist data, independent of the container’s life cycle.


Uses of Volumes
-For example your container runs an app that has many logfiles.
You can store logfiles in a volume, so you can access those logfiles even when the container is shutdown or after you have destroyed the container.
- Testing : you might mount a source folder, and see what affects it has, as you make changes to the source code.
-Decouple data stored from the container 



A.  Adding a data volume


docker run --name vub -it -v /root/aman:/root/aman -t ubuntu /bin/bash
 
root@localhost:/# cd /var/lib/docker/volumes



docker inspect vub 
docker inspect '{​​​​​{​​​​​ .Mounts }​​​​​}​​​​​' vub


Let's remove the container
docker rm vub
and verify


VOLUMES IN DOCKERFILE
VOLUME /myvol
VOLUME /myvol1 /myvol2


5.    DATA VOLUME CONTAINER
This is very useful if you want to share data between containers or you want to use the data from non-persistent containers. 
We will first create a container (container1) and mount a volume inside of that:


docker run --name vub -it -v /root/aman25 ubuntu /bin/bash


Now, let us launch another container (container2) but it will mount the data volume from container1 as given below:


docker run -it --volumes-from vub --name vub_ref ubuntu /bin/bash



docker run -it ubuntu /bin/bash


docker create -it ubuntu /bin/bash
docker start contid


VOLUME /var/www/html


docker build -t amanvol .
docker images | grep amanvol
=====================================================================



Migration of data in containers ( using Data volumes and data volume containers)

SOURCE container
docker run --name vub -it -v /project/app ubuntu /bin/bash

STEP 1: BACKUP 

Intermediate container

docker run --volumes-from vub -v $(pwd):/backup -it ubuntu tar cvf /backup/backup.tar /project


Here we’ve launched a new container and mounted the volume from the source container. 
We’ve then mounted a local host directory as /backup. 
Finally, we’ve passed a command that uses tar to backup the contents of the vub volume to a backup.tar file inside our 
/backup directory. 

===============================

STEP 2: Restore

Share the tar file to host where you want to migrate data...

Destination container:
docker run -it -v /restored --name destination ubuntu /bin/bash

RESTORE: Intermediate container..

docker run --volumes-from destination -v $(pwd):/backup ubuntu bash -c "cd /restored && tar xvf /backup/backup.tar"
 


 
==================================

ECR and ECS:
https://www.qwiklabs.com/focuses/15511?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=10869977

 
