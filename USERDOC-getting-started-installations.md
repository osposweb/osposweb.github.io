This document are made for quick deploy/usage, for detailed instructions please read the section of [Installation and requirements (click here)](OSPOS-development-index#tech-installation) wiki page

* [Quick Own Local Deploy installation](#local-deploy-install)
* [Fast Cloud Deploy installation](#cloud-deploy-installation)
* [More advance and customized installations](#more-advance-and-customized-installations)

# Local Deploy install
----------------------

Its the best option to most customized and controlled, also as counterpart you are on your own, 
but its totally free of charge of course! and most cheap and optimized. We must use Linux 
a [Debian live image ready to use](https://www.debian.org/CD/live/#live-install-stable) or 
a [Devuan live image ready to use](https://devuan.org/os/documentation/install) derivate distribution OS, 
for more detailed instructions read the section of [Installation and requirements (click here)](OSPOS-development-index#tech-installation).

1. Log in to the OS and/or open a terminal, type `sudo su` to scale privileges.
2. Install **apache2**, **php** and **mariadb** `apt-get install apache2 mariadb-server php php-curl php-gd php-intl`
3. run download command `wget https://github.com/opensourcepos/opensourcepos/archive/3.1.1.tar.gz -O ospos311.tar.gz`
4. uncompress with command `tar zxvf ospos311.tar.gz  --strip 1 -C /var/www/html`
5. create the database with `mysql -u root -e 'CREATE SCHEMA ospos'`
6. populate database with command `mysql -u root ospos < /var/www/html/application/database/database.sql`
7. configure user credentials to database with `sed -i "s/admin/root/g" /var/www/html/application/config/database.php`
7. configure password database with `sed -i "s/pointofsale//g" /var/www/html/application/config/database.php`
7. open the web browser and run from `http://localhost/public` of `http://YOURIPADDRESS/public`
8. login by using username as **admin**  and the password are **pointofsale**
9. Enjoy and remenber to point `YOURIPADDRESS` to your installation server.

**IMPORTANT** first login will have a delay due "send statics" are activated in `"Office->Store config->General->Send statics"`, deactivate when login if you not have enough network or internet.

This was a quick fast local installation, for professional install more steps must be take in care such database protection and web server performance.

# Cloud Deploy installation
-------------

If you want to run a quick demo of OSPOS the most quick way its using [`DigitalOcean` (click here)](https://m.do.co/c/ac38c262507b), a full setup will only take about 2 minutes by following steps below.

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

**IMPORTANT** first login will have a delay due "send statics" are activated this only happened at the first login.

More info [on maintaining a docker](https://github.com/opensourcepos/opensourcepos/wiki/Docker-cloud-maintenance) install can be found on the wiki

# More advance and customized installations

Please refers to the [OSPOS installation development requirements wiki page (click here)](OSPOS-development-index#requirements) for complete info about installations

> If you like the project, and you are making money out of it on a daily basis, then consider buying us a coffee so I can keep adding features. [![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MUN6AEG7NY6H8)

