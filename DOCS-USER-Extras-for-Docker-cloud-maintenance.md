Docker cloud instances can be directly maintained through the docker-cloud command tool. Most of the basic operations are available from the docker-cloud web frontend.

**NOTE** This its not end-user oriented task, need some level of knowledge specially in unix-linux like operating systems.

# 1. Local install using Docker
--------------------------

From now on ospos can be deployed using Docker on Linux, Mac or Windows. This setup dramatically reduces the number of possible issues as all setup is now done in a Dockerfile. Docker runs natively on mac and linux, but will require more overhead on windows. Please refer to the docker documentation for instructions on how to set it up on your platform.

To build and run the image, issue following commands in a terminal with docker installed

    docker-compose build
    docker-compose up 


# 2. Cloud install using Docker
--------------------------

If you want to run a quick demo of ospos or run it permanently in the cloud, then we
suggest using Docker cloud together with the DigitalOcean hosting platform. This way all the
configuration is done automatically and the install will just work. 

If you choose *DigitalOcean* [through this link](https://m.do.co/c/ac38c262507b), you will get a *$10 credit* for a first
month of uptime on the platform. A full setup will only take about 2 minutes by following steps below.

1. Create a [Digitalocean account](https://m.do.co/c/ac38c262507b)
2. Create a [docker cloud account](https://cloud.docker.com)
3. Login to docker cloud
4. Associate your docker cloud account with your previously created digital ocean account under settings
5. Create a new node on DigitalOcean through the `Infrastructure > Nodes` tab. Fill in a name (ospos) and choose a region near to you. We recommend to choose a node with minimum 1G RAM for the whole stack
6. Click [![Deploy to Docker Cloud](https://files.cloud.docker.com/images/deploy-to-dockercloud.svg)](https://cloud.docker.com/stack/deploy/?repo=https://github.com/opensourcepos/opensourcepos) 
7. Othewise create a new stack under `Applications > Stacks` and paste the [contents of docker-cloud.yml](https://github.com/opensourcepos/opensourcepos/blob/master/docker-cloud.yml) from the source repository in the text field and hit `Create and deploy` 
8. Find your website url under `Infrastructure > Nodes > <yournode> > Endpoints > web`
9. Login with default username/password admin/pointofsale
10. DNS name for this server can be easily configured in the DigitalOcean control panel

More info [on maintaining a docker](https://github.com/opensourcepos/opensourcepos/wiki/Docker-cloud-maintenance) install can be found on the wiki


# 3. Maintaining a Docker cloud install
----------------------------------
Docker cloud will save all data in docker volumes that are stored apart from the actual containers. This makes it easy to stay on the latest version of an opensourcepos image. The cloud UI offers some options to configure autoredeploy once a new commit is made.


## 3.1 How to configure autodeploy

Autoredeploy can be triggered in the docker cloud webapp. Go to the container tab in the left and select the web container. Then choose redeploy in the top dropdown. Docker cloud will now ask to redeploy with the latest image and keep or trash persisted data.

## 3.2 Running mysql sripts with dockers

### 3.2.1 How to run a mysql script using docker-cloud cli on a local setup

If you need to run a manual sql statement on a docker cloud deployed mariadb, then you will first need to install the docker-cloud cli. This is a python program that [can be installed using pip](https://docs.docker.com/docker-cloud/installing-cli/), the python package manager using 

`pip install docker-cloud`

Next you will need to open a shell on the mysql docker container in order to execute the sql.

`docker-cloud container exec mysql-1 /bin/bash`

This should open a new prompt inside the mysql container. A mysql client is preconfigured and available in that environment. Start the client as follows

`mysql -c 'use ospos';`

At this point any sql query can be executed on the database. Don't forget to backup first in case you're planning to upgrade!

### 3.2.2 How to run a mysql script through digitalocean's console

* Log into Digital Ocean Console through these instructions: https://www.digitalocean.com/community/tutorials/how-to-use-the-digitalocean-console-to-access-your-droplet I have tried this with both Abrowser (Firefox-based) and Chromium (Chrome-based) and the scroll bar doesn't seem to work with Abrowser, so for me Chromium is the preferred browser for this
* Alternatively, log into the server using SSH after creating a root password
* Install docker-cloud CLI if you have not yet done so: Enter `docker run dockercloud/cli -h`
* Next you need to find out the exact names of your MySQL container. You can find it under "Containers" in the Docker web UI or you can find it out by running the command `docker run -it -v ~/.docker:/root/.docker:ro --rm dockercloud/cli container ps` You are looking for the name in the left-most column called "NAME"
* To log into the container, enter `docker run -it -v ~/.docker:/root/.docker:ro --rm dockercloud/cli exec [container name] /bin/bash
* Enter `mysql -u root -ppointofsale`
* Enter `use ospos`