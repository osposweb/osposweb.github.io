Docker cloud instances can be directly maintained through the docker-cloud command tool. Most of the basic operations are available from the docker-cloud web frontend. 

Maintaining a Docker cloud install
----------------------------------
Docker cloud will save all data in docker volumes that are stored apart from the actual containers. This makes it easy to stay on the latest version of an opensourcepos image. The cloud UI offers some options to configure autoredeploy once a new commit is made.

How to configure autodeploy
---------------------------------
Autoredeploy can be triggered in the docker cloud webapp. Go to the container tab in the left and select the web container. Then choose redeploy in the top dropdown. Docker cloud will now ask to redeploy with the latest image and keep or trash persisted data.

How to run a mysql script 
----------------------------
If you need to run a manual sql statement on a docker cloud deployed mariadb, then you will first need to install the docker-cloud cli. This is a python program that [can be installed using pip](https://docs.docker.com/docker-cloud/installing-cli/), the python package manager using 

`pip install docker-cloud`

Next you will need to open a shell on the mysql docker container in order to execute the sql.

`docker-cloud container exec mysql-1 /bin/bash`

This should open a new prompt inside the mysql container. A mysql client is preconfigured and available in that environment. Start the client as follows

`mysql -c 'use ospos';`

At this point any sql query can be executed on the database. Don't forget to backup first in case you're planning to upgrade!