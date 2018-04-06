This document are made for quick deploy/usage, for detailed instructions please read [OSPOS installations index (click here)](OSPOS-development-index#1---officially-supported).

* 🖫 [Local Install](#local-install)
  * 💻 [Own Local Deploy Install](#local-deploy-install)
  * 🖳 [Local Docker Deploy Install](#local-docker-install)
* 📶 [Cloud Install](#cloud-install)
  * 🖧 [Cloud Deploy Installation](#cloud-deploy-installation)
  * 🖯 [Cloud Docker Installation](#cloud-docker-install)

**After read this read also [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)** 

# Local Install
----------------------

Its the best option to most customized and controlled, as counterpart you are by your own. We recommended using the way of system package vendor, due Docker option needs advanced Linux/Mac knowledge.

## Local Deploy install

We assumed a *nix like environment, (as MAc or Linux does) due most vendors and hosting only provided that kind of environment.

1. **Terminal** windows must be open: in MacOSX at Finder->Accesories->Terminal in Linux at Menu->SystemTools->Terminal, then a window with prompt will show, in Linux flavors must gain root access with `sudo su` command
2. **Dependences** install: Apache2, MariaDB, PhP with openssl/mcrypt, curl, gd, intl and bcmath, in MAC all included in MAMP, in Linux for Deb and RPM based distribution are `apt-get install apache2 mariadb-server php5-curl php5-mysql php5-gd php5-intl` or/and `yum install httpd mysql-server php php-bcmath php-dba php-gd` respectively, recent debian not use "php5" only "php" in their names of the packages. Now enable the mod-rewrite module by `a2enmod rewrite` command.
3. **Htdocs** working directory: this it's change the working directory in the current terminal window, assuming the `/var/www/html` as the web root html document directory and you can move to by executing `cd /var/www/html` but remenber this depends of the Operating System Apache2 install
4. **Download** executing in same terminal: `wget https://github.com/opensourcepos/opensourcepos/archive/lasted.tar.gz -O osposlastedstable.tar.gz` to later move to the htdoc directory.
5. **Uncompress** to htdocs the download: `tar zxvf osposlastedstable.tar.gz  --strip 1 -C /var/www/html` this will populate all the web server htdocs root directory only for the software.
6. **Create** database and access: executing in same terminal `mysql -u root -e "CREATE SCHEMA ospos;CREATE USER 'admin'@'%' IDENTIFIED BY 'pointofsale';CREATE DATABASE ospos;GRANT ALL PRIVILEGES ON ospos . * TO 'admin'@'%' IDENTIFIED BY 'poinofsale' WITH GRANT OPTION;FLUSH PRIVILEGES;"`
7. **Populate** database with that other command in same terminal `mysql -u admin -ppointofsale -D ospos < /var/www/html/application/database/database.sql`
8. **Configure** the OSPOS index page and encription key, this its by editing the config and htaccess files, can be bypassing but strong recommended set the encryption key at `application/config/config.php` with your owcurrently for security.
9. **Browsing** using the web browser and run from `http://localhost/public` or better `http://127.0.0.1/public` 
10. **Login** by using username as **admin**  and the password are **pointofsale** and then enjoy the software.

For those that only want to try an easy option could be a live operating system image ready to use with all included **without OS install need** that can be downloaded with all need components included and software ready to use at https://sourceforge.net/projects/vegnuli/files/VenenuX-1.0/venenux-1.0-osposweb/debian-venenux-8-osposweb-i386.hybrid.iso/download and can later boot in a virtualBox machine by example.

Now next to [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)

## Local Docker install

Docker deploy its a *nix like environment due Docker runs natively on mac and linux. Please refer to the docker documentation for instructions on how to set it up on your platform.

1. **Terminal** windows must be open: in MacOSX at Finder->Accesories->Terminal in Linux at Menu->SystemTools->Terminal, then a window with prompt will show, in Linux flavors must gain root access only for next step with `sudo su` command
2. **Dependences** install: docker.io, in MAC all included in `docker.img` file by launching it, drag Moby the whale to the Applications folder and later relaunch service from Finder, in Linux for Deb and RPM based distribution are `apt-get install docker.io` or/and `yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo;yum install -y docker-ce` respectively, oldstable deb distributions may need "backports" or "external" repositories. After install hit "CRTL+D" to out from root account.
3. **Dockerplace** working directory for the dockerfile of ospos: this it's change the working directory in the current terminal window, assuming the `~` represent your home with a docker root document directory and you can move to by executing `mkdir ~/osposdicker;cd ~/osposdocker` but remenber this depends of the Operating System Docker install too.
4. **Download** executing in same terminal: `wget https://github.com/opensourcepos/opensourcepos/archive/lasted.tar.gz -O osposlastedstable.tar.gz` to later move to the htdoc directory.
5. **Uncompress** to htdocs the download: `tar zxvf osposlastedstable.tar.gz  --strip 1 -C ~/osposdicker` this will populate all the docker root image directory only for the software.
6. **Build+Run** the image with following commands `docker-compose build` and then later `docker-compose up`

Now next to [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage) More info in the wiki page [Extras for Docker cloud maintenance](DOCS-USERS-Extras-for-Docker-cloud-maintenance) must be read.

If you want to run from the latest git source, then use docker and composer to run the build

`docker run --rm -v $(pwd):/app composer/composer install` \
`docker run --rm -v $(pwd):/app -w /app lucor/php7-cli php bin/install.php translations develop` \
`docker run --rm -it -v $(pwd):/app -w /app digitallyseamless/nodejs-bower-grunt "sh -c npm install && bower install"` \
`docker-compose build` \
`docker-compose up`

More info in the wiki page [Extras for Docker cloud maintenance](DOCS-USERS-Extras-for-Docker-cloud-maintenance) must be read.

## See also:

* [Getting Started with Open Source POS](home)
  * [OSPOS Feature datasheet and usage](OSPOS-complete-feature-datasheet)
  * [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)
  * [OSPOS Printing general info](DOCS-USERS-for-OSPOS-Printing)

# Cloud Install
-------------

Best choice its free/private VPS, this due free hosting and mayority of private dont provide necesary enabled php modules such "openssl" and "curl" as examples, only some very older accounts still can access those modules. We recomended Digital Ocean

## Cloud Deploy installation

For Cloud hosting the most compatible way it's using [`DigitalOcean` (click here)](https://m.do.co/c/ac38c262507b) as the recommended way if need hosting related.

1. **Create** a [Digitalocean account](https://m.do.co/c/ac38c262507b) and once complete go log in.
2. **Choose** a Debian Droplet by click the Create button in the top right hand corner, and later from the dropdown menu.
3. **OneClickApp** as the LAMP on 9 app, clik the One click apps link. Scroll down, and choose a size. Then scroll down to Choose a datacenter region. Select the region closest to you. Finally select hosname as `osposdo`
4. **Connecting**: Now click the Create button to create your droplet. When your droplet has been created, you'll receive an email from DigitalOcean. This will have the information to log in. You now have the information needed to log in to your server. If you have Mac or Linux, you can use the built-in terminal program SSH as `ssh root@<digitalocean's-ip>`.
5. **Install** software, apache and mysql/mariadb are already, need enable the mod-rewrite module by `a2enmod rewrite` then PHP modules by `apt-get install php7.0-intl php7.0-mcrypt php7.0-bcmath php7.0-curl` Type "Y" when it asks if you want to continue. Finally restart service by `service apache2 restart`
6. **Download** executing in same terminal: `wget https://github.com/opensourcepos/opensourcepos/archive/lasted.tar.gz -O osposlastedstable.tar.gz` to later move to the htdoc directory.
7. **Uncompress** to htdocs the download: `tar zxvf osposlastedstable.tar.gz  --strip 1 -C /var/www/html` this will populate all the web server htdocs root directory only for the software.
8. **Create** database and access: executing in same terminal `mysql -u root -p -e "CREATE SCHEMA ospos;CREATE USER 'admin'@'%' IDENTIFIED BY 'pointofsale';CREATE DATABASE ospos;GRANT ALL PRIVILEGES ON ospos . * TO 'admin'@'%' IDENTIFIED BY 'poinofsale' WITH GRANT OPTION;FLUSH PRIVILEGES;"` the DigitalOcean's password are in the filesystem, get with `cat /root/.digitalocean_password` command before.
9. **Populate** database with that other command in same terminal `mysql -u admin -ppointofsale -D ospos < /var/www/html/application/database/database.sql`
10. **Configure** the OSPOS index page and encription key, this its by editing the config and htaccess files, can be bypassing but strong recommended set the encryption key at `application/config/config.php` with your owcurrently for security.
11. **Browsing** using the web browser and run from `http://<digitalocean-ip>/public` changing the "digitalocean-ip" with that provided in the mail previously received.
12. **Login** by using username as **admin**  and the password are **pointofsale** and then enjoy the software.

Now next to [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)

## Cloud Docker install

Not recomended for begginers. We recomended Digital Ocean:

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

Now next to [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)

More info in the wiki page [Extras for Docker cloud maintenance](DOCS-USERS-Extras-for-Docker-cloud-maintenance) must be read.

# See also:

* [Getting Started with Open Source POS](home)
  * [OSPOS Feature datasheet and usage](OSPOS-complete-feature-datasheet)
  * [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)
  * [OSPOS Printing general info](DOCS-USERS-for-OSPOS-Printing)
* [OSPOS requirements data sheet](OSPOS-development-index#requirements)
* [Extras for Docker cloud maintenance](DOCS-USER-Extras-for-Docker-cloud-maintenance)
