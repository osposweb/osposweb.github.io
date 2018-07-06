
* 🖫 [Local Install](#local-install)
  * 💻 [Own Local Deploy Install](#local-deploy-install)
  * 🖳 [Local Docker Deploy Install](#local-docker-install)
* 📶 [Cloud Install](#cloud-install)
  * 🖧 [Cloud Deploy Installation](#cloud-deploy-installation)
* [Professional Install](#professional-install)
  * [Local Professional Install](#professional-local-install)
  * [Others OSs Install guides](#others-oss-install-guides)

**After read this read also [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)** 

## Installation notes for impatients

**Dont use github direclty!!** For those that want to try an easy option that can be **downloaded with all needed components included and software ready to use at https://sourceforge.net/projects/vegnuli/files/VenenuX-1.0/venenux-1.0-osposweb/debian-venenux-8-osposweb-i386.hybrid.iso/download** and can later boot in a virtualBox machine by example.

**WARNING** Ospos has specific requirements and not all hosting providers will offer what is needed. For more detailed **requirements see: [OSPOS requirements datasheet](OSPOS-development-index#requirements) and then go back here**. For example **softaculus** is not supported by this community and has nothing to do with the project.

# Local Install
----------------------

We advise to follow instructions here as closely as possible, otherwise we won't be able to support you in case of issues. **Dont use github direclty!!**

## Local Deploy install

We assume a *nix like environment, (like Mac or Linux) as this is the most comonly used for web application deployments.

1. **Terminal** windows must be open: in MacOSX at Finder->Accesories->Terminal in Linux at Menu->SystemTools->Terminal, then a window with prompt will show, in Linux flavors must gain root access with `sudo su` command
2. **Dependences** install: Apache2, MariaDB, PhP with openssl/mcrypt, curl, gd, intl and bcmath, in MAC all included in MAMP, in Linux for Deb and RPM based distribution are `apt-get install apache2 mariadb-server php5-curl php5-mysql php5-gd php5-intl` or/and `yum install httpd mysql-server php php-bcmath php-dba php-gd` respectively, recent debian not use "php5" only "php" in their names of the packages. Now enable the mod-rewrite module by `a2enmod rewrite` command.
3. **Htdocs** working directory: this it's change the working directory in the current terminal window, assuming the `/var/www/html` as the web root html document directory and you can move to by executing `cd /var/www/html` but remenber this depends of the Operating System Apache2 install
4. **Download** please **Dont use github direclty!!** and then executing in same terminal: `wget https://github.com/opensourcepos/opensourcepos/archive/lasted.tar.gz -O osposlastedstable.tar.gz` to later move to the htdoc directory. 
5. **Uncompress** to htdocs the download: `tar zxvf osposlastedstable.tar.gz  --strip 1 -C /var/www/html` this will populate all the web server htdocs root directory only for the software.
6. **Create** database and access: executing in same terminal `mysql -u root -e "CREATE SCHEMA ospos;CREATE USER 'admin'@'%' IDENTIFIED BY 'pointofsale';CREATE DATABASE ospos;GRANT ALL PRIVILEGES ON ospos . * TO 'admin'@'%' IDENTIFIED BY 'poinofsale' WITH GRANT OPTION;FLUSH PRIVILEGES;"`
7. **Populate** database with that other command in same terminal `mysql -u admin -ppointofsale -D ospos < /var/www/html/application/database/database.sql`
8. **Configure** the OSPOS index page and encription key, this its by editing the config and htaccess files, can be bypassing but strong recommended set the encryption key at `application/config/config.php` with your owcurrently for security.
9. **Browsing** using the web browser and run from `http://localhost/public` or better `http://127.0.0.1/public` 
10. **Login** by using username as **admin**  and the password are **pointofsale** and then enjoy the software.

Now next to [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)

For those that want to try an easy option can be downloaded with all need components included and software ready to use at https://sourceforge.net/projects/vegnuli/files/VenenuX-1.0/venenux-1.0-osposweb/debian-venenux-8-osposweb-i386.hybrid.iso/download and can later boot in a virtualBox machine by example.

## Local Docker install

Docker deploy its a *nix like environment due Docker runs natively on mac and linux.

1. **Terminal** windows must be open: in MacOSX at Finder->Accesories->Terminal in Linux at Menu->SystemTools->Terminal, then a window with prompt will show, in Linux flavors must gain root access only for next step with `sudo su` command
2. **Dependences** install: docker.io, please refer to the docker documentation for better instructions: in MAC all included in `docker.img` file by launching it, drag Moby the whale to the Applications folder and later relaunch service from Finder, in Linux for Deb and RPM based distribution are `apt-get install docker.io` or/and `yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo;yum install -y docker-ce` respectively, oldstable deb distributions may need "backports" or "external" repositories. After install hit "CRTL+D" to out from root account.
3. **Dockerplace** working directory for the dockerfile of ospos: this it's change the working directory in the current terminal window, assuming the `~` represent your home with a docker root document directory and you can move to by executing `mkdir ~/osposdicker;cd ~/osposdocker` but remenber this depends of the Operating System Docker install too.
4. **Download** please **Dont use github direclty!!** and executing in same terminal: `wget https://github.com/opensourcepos/opensourcepos/archive/lasted.tar.gz -O osposlastedstable.tar.gz` to later move to the htdoc directory.
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

Best choice its free/private VPS, this due free hosting and mayority of private dont provide necesary enabled php modules such "openssl" and "curl" as examples, only some very older accounts still can access those modules. We recomended Digital Ocean. Ancient accounts of Hostinger have those all enabled.

## Cloud Deploy installation

For Cloud hosting we recommend [`DigitalOcean` (click here)](https://m.do.co/c/ac38c262507b) if need hosting related.

1. **Create** a [Digitalocean account](https://m.do.co/c/ac38c262507b) and once complete go log in.
2. **Choose** a Debian Droplet by click the Create button in the top right hand corner, and later from the dropdown menu.
3. **OneClickApp** as the LAMP on 9 app, clik the One click apps link. Scroll down, and choose a size. Then scroll down to Choose a datacenter region. Select the region closest to you. Finally select hosname as `osposdo`
4. **Connecting**: Now click the Create button to create your droplet. When your droplet has been created, you'll receive an email from DigitalOcean. This will have the information to log in. You now have the information needed to log in to your server. If you have Mac or Linux, you can use the built-in terminal program SSH as `ssh root@<digitalocean's-ip>`.
5. **Install** software, apache and mysql/mariadb are already, need enable the mod-rewrite module by `a2enmod rewrite` then PHP modules by `apt-get install php7.0-intl php7.0-mcrypt php7.0-bcmath php7.0-curl` Type "Y" when it asks if you want to continue. Finally restart service by `service apache2 restart`
6. **Download** please **Dont use github direclty!!**, and executing in same terminal: `wget https://github.com/opensourcepos/opensourcepos/archive/lasted.tar.gz -O osposlastedstable.tar.gz` to later move to the htdoc directory.
7. **Uncompress** to htdocs the download: `tar zxvf osposlastedstable.tar.gz  --strip 1 -C /var/www/html` this will populate all the web server htdocs root directory only for the software.
8. **Create** database and access: executing in same terminal `mysql -u root -p -e "CREATE SCHEMA ospos;CREATE USER 'admin'@'%' IDENTIFIED BY 'pointofsale';CREATE DATABASE ospos;GRANT ALL PRIVILEGES ON ospos . * TO 'admin'@'%' IDENTIFIED BY 'poinofsale' WITH GRANT OPTION;FLUSH PRIVILEGES;"` the DigitalOcean's password are in the filesystem, get with `cat /root/.digitalocean_password` command before.
9. **Populate** database with that other command in same terminal `mysql -u admin -ppointofsale -D ospos < /var/www/html/application/database/database.sql`
10. **Configure** the OSPOS index page and encription key, this its by editing the config and htaccess files, can be bypassing but strong recommended set the encryption key at `application/config/config.php` with your owcurrently for security.
11. **Browsing** using the web browser and run from `http://<digitalocean-ip>/public` changing the "digitalocean-ip" with that provided in the mail previously received.
12. **Login** by using username as **admin**  and the password are **pointofsale** and then enjoy the software.

Now next to [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)

More info in the wiki page [Extras for Docker cloud maintenance](DOCS-USERS-Extras-for-Docker-cloud-maintenance) must be read.

# Professional Install
-----------------------

This section its dedicated to those that will deploy in secure and serious production environments. **Dont use github direclty!!** Downloads must be using unstable bintray or stable releases checkpoints.

## Professional Install Local

Professional install will assumed behing a complex network, that will **redirect the port and the path of the OSPOS installation** due a front webserver will receive the request and firewall/reverseproxy will redirect to the ospos server install place.
* If you **will use reverse proxy redirection** due there's no need of a installed firewall in the local webserver OS, that are under a DMZ zone.
* If you **dont want hiyacked all the root of your webserver**, can defined  new port and to that port a new webroot htdocs place where the OSPOS software will reside away of the normal webserver installation.

(WIP)

# Other Install guides

Currently only Apache & MySql/MariaDB are officialy supported but this will or may be changed in the future:

* https://github.com/opensourcepos/opensourcepos/wiki/Installing-on-Raspberry-PI---Orange-PI-(Headless-OSPOS)
* [OSPOS install lighttpd and mariadb debian like](OSPOS-install-lighttpd-and-mariadb-debian-like)
* https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-LEMP
* https://github.com/opensourcepos/opensourcepos/wiki/Deployment-of-OSPOS-with-LEMP-on-Raspberry-Pi-3-Model-B
* https://github.com/opensourcepos/opensourcepos/wiki/Development-setup
* https://github.com/opensourcepos/opensourcepos/wiki/Installing-%22opensourcepos%22-in-windows-and-localhost
* https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-MAMP-for-Windows
* https://github.com/opensourcepos/opensourcepos/wiki/OSPOS-using-Xampp-(recommended-for-testing-or-local-use-only).

# See also:

* [Getting Started with Open Source POS](home)
  * [OSPOS Feature datasheet and usage](OSPOS-complete-feature-datasheet)
  * [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)
  * [OSPOS Printing general info](DOCS-USERS-for-OSPOS-Printing)
* [OSPOS requirements data sheet](OSPOS-development-index#requirements)
* [Extras for Docker cloud maintenance](DOCS-USER-Extras-for-Docker-cloud-maintenance)

For those that want to try an easy option can be downloaded with all need components included and software ready to use at https://sourceforge.net/projects/vegnuli/files/VenenuX-1.0/venenux-1.0-osposweb/debian-venenux-8-osposweb-i386.hybrid.iso/download and can later boot in a virtualBox machine by example.
