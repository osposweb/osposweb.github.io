Docker maintenance need some level of knowledge of unix-like operating systems. 

# 1. Install using Docker
--------------------------

From now on ospos can be deployed using Docker on Linux, Mac or Windows. This setup dramatically reduces the number of possible issues as all setup is now done in a Dockerfile. Docker runs natively on mac and linux, but will require more overhead on windows. Please refer to the docker documentation for instructions on how to set it up on your platform.

See wiki pages for:
1. [OSPOS DOCS USERS Local Docker install](DOCS-USERS-Getting-Started-installations#local-docker-install)
2. [OSPOS DOCS USERS Cloud Docker install](DOCS-USERS-Getting-Started-installations#cloud-docker-install)

# 2. Maintaining a Docker cloud install
----------------------------------
Docker cloud will save all data in docker volumes that are stored apart from the actual containers. This makes it easy to stay on the latest version of an opensourcepos image. The cloud UI offers some options to configure autoredeploy once a new commit is made.


## 2.1 How to configure autodeploy

Autoredeploy can be triggered in the docker cloud webapp. Go to the container tab in the left and select the web container. Then choose redeploy in the top dropdown. Docker cloud will now ask to redeploy with the latest image and keep or trash persisted data.

## 2.2 Running mysql sripts with dockers

### 2.2.1 How to run a mysql script using docker-cloud cli on a local setup

If you need to run a manual sql statement on a docker cloud deployed mariadb, then you will first need to install the docker-cloud cli. This is a python program that [can be installed using pip](https://docs.docker.com/docker-cloud/installing-cli/), the python package manager using 

`pip install docker-cloud`

Next you will need to open a shell on the mysql docker container in order to execute the sql.

`docker-cloud container exec mysql-1 /bin/bash`

This should open a new prompt inside the mysql container. A mysql client is preconfigured and available in that environment. Start the client as follows

`mysql -c 'use ospos';`

At this point any sql query can be executed on the database. Don't forget to backup first in case you're planning to upgrade!

### 2.2.2 How to run a mysql script through digitalocean's console

* Log into Digital Ocean Console through these instructions: https://www.digitalocean.com/community/tutorials/how-to-use-the-digitalocean-console-to-access-your-droplet I have tried this with both Abrowser (Firefox-based) and Chromium (Chrome-based) and the scroll bar doesn't seem to work with Abrowser, so for me Chromium is the preferred browser for this
* Alternatively, log into the server using SSH after creating a root password
* Install docker-cloud CLI if you have not yet done so: Enter `docker run dockercloud/cli -h`
* Next you need to find out the exact names of your MySQL container. You can find it under "Containers" in the Docker web UI or you can find it out by running the command `docker run -it -v ~/.docker:/root/.docker:ro --rm dockercloud/cli container ps` You are looking for the name in the left-most column called "NAME"
* To log into the container, enter `docker run -it -v ~/.docker:/root/.docker:ro --rm dockercloud/cli exec [container name] /bin/bash
* Enter `mysql -u root -ppointofsale`
* Enter `use ospos`