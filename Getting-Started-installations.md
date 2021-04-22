* 🖫 [Local Install](#local-install)
  * 💻 [Own Local Deploy Install](#local-deploy-install)
  * 🖳 [Local Docker Deploy Install](#local-docker-install)
* 📶 [Cloud Install](#cloud-install)
  * 🖧 [Cloud Deploy Installation](#cloud-deploy-installation)
* ⌨ [cPanel & SSH Installer](#cpanel-ssh-install)
* [Professional Install](#professional-install)
  * [Local Professional Install](#professional-local-install)
  * [Others OSs Install guides](#other-install-guides)

**After reading this read also [Getting Started Usage](Getting-Started-usage)** 

# Installation
----------------------

Please follow the instructions here as closely as possible, otherwise we won't be able to support you in case of issues.

___We will be installing a prebuilt version of OSPOS.  Do not click on the Green "Clone or Download" button found in the Code view of GitHub.  It is NOT a working copy of OSPOS.  Instead, in the following instructions, we will be retrieving and installing a prebuilt official release.___

## Local Deploy install for Unix/Linux environments.

1. **Terminal** windows must be open: in MacOSX at Finder->Accesories->Terminal in Linux at Menu->SystemTools->Terminal, then a window with prompt will show, it's best to elevate to root access with `sudo su` command.

2. **Dependencies** Install: Apache2, MariaDB, PhP with openssl, curl, gd, intl and bcmath, in MAC all these are included in MAMP, in Linux for Deb and RPM based distribution you need `apt-get install apache2 mariadb-server php7.4-curl php7.4-mysql php7.4-gd php7.4-intl php7.4-openssl` or/and `yum install httpd mysql-server php php-bcmath php-dba php-gd php-openssl`. Debian does not use "php7.4" bit "php" in their names of the packages. Now finally enable the mod-rewrite module by entering the `a2enmod rewrite` command.

3. **Htdocs** working directory: Change the working directory in the current terminal window, assuming the `/var/www/html` as the web root html document directory and you can move to by executing `cd /var/www/html` but remember this depends of the Operating System Apache2 install

4. **Download** the latest version of from the release section and uncompress it to the htdoc directory

5. **Create** database and access: executing in same terminal `mysql -u root -e "CREATE SCHEMA ospos;CREATE USER 'admin'@'%' IDENTIFIED BY 'pointofsale';GRANT ALL PRIVILEGES ON ospos . * TO 'admin'@'%' IDENTIFIED BY 'pointofsale' WITH GRANT OPTION;FLUSH PRIVILEGES;"` take **in consideratin password administrative privilegies** for the database users.

6. **Populate** database with that other command in same terminal `mysql -u admin -ppointofsale -D ospos < /var/www/html/database/database.sql`

7. **Browse** use the web browser and run from `http://localhost/public` or better `http://127.0.0.1/public` 

8. **Login** by using username as **admin** and the password **pointofsale** and then enjoy the software.

Now next to [Getting Started Usage](Getting-Started-usage)

## Local Docker install

1. **Terminal** windows must be open: in MacOSX at Finder->Accesories->Terminal in Linux at Menu->SystemTools->Terminal, then a window with prompt will show, in Linux flavors must gain root access only for next step with `sudo su` command

2. **Dependencies** install: docker.io, please refer to the docker documentation for better instructions: in MAC all included in `docker.img` file by launching it, drag Moby the whale to the Applications folder and later relaunch service from Finder, in Linux for Deb and RPM based distribution are `apt-get install docker.io` or/and `yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo;yum install -y docker-ce` respectively, oldstable deb distributions may need "backports" or "external" repositories. After install hit "CRTL+D" to exit the root shell.

3. **Dockerplace** working directory for the dockerfile of ospos: this change the working directory in the current terminal window, assuming the `~` represent your home with a docker root document directory and you can move to by executing `mkdir ~/osposdocker;cd ~/osposdocker`.

4. **Download** the latest version of from the release section and uncompress it to the htdoc directory

5. **Build+Run** the image with following commands `docker-compose build` and then later `docker-compose up`, take **in consideration password administrative privileges** for the database users.

Now next to [Getting Started Usage](Getting-Started-usage) More info in the wiki page [Extras for Docker cloud maintenance](Extras-for-Docker-cloud-maintenance) must be read.

## See also:

* [Getting Started with Open Source POS](home)
  * [Feature datasheet and usage](complete-feature-datasheet)
  * [Getting Started Usage](Getting-Started-usage)
  * [Printing general info](Printing)

# Cloud Install
-------------

## Cloud Deploy installation

For Cloud hosting we recommend [`DigitalOcean` (click here)](https://m.do.co/c/ac38c262507b) where you will get a **$100 free credit** and send a referral back to the project as a donation!

1. **Create** a [Digitalocean account](https://m.do.co/c/ac38c262507b) and once complete go log in.

2. **Choose** a Debian Droplet by click the Create button in the top right hand corner, and later from the dropdown menu.

3. **OneClickApp** as the LAMP on 9 app, clik the One click apps link. Scroll down, and choose a size. Then scroll down to Choose a datacenter region. Select the region closest to you. Finally select a hostname as `osposdo`

4. **Connecting**: Now click the Create button to create your droplet. When your droplet has been created, you'll receive an email from DigitalOcean. This will have the information to log in. You now have the information needed to log in to your server. If you have Mac or Linux, you can use the built-in terminal program SSH as `ssh root@<digitalocean's-ip>`.

5. **Install** software, apache and mysql/mariadb are already there. You only need to enable the mod-rewrite module by `a2enmod rewrite` then PHP modules by `apt-get install php-intl php-openssl php-bcmath php-curl` Type "Y" when it asks if you want to continue. Finally restart service by `service apache2 restart`

6. **Download** the latest version of from the release section and uncompress it to a directory of choice

7. **Create** database and access: executing in same terminal `mysql -u root -p -e "CREATE SCHEMA ospos;CREATE USER 'admin'@'%' IDENTIFIED BY 'pointofsale';GRANT ALL PRIVILEGES ON ospos . * TO 'admin'@'%' IDENTIFIED BY 'pointofsale' WITH GRANT OPTION;FLUSH PRIVILEGES;"` the DigitalOcean's password are in the filesystem, get with `cat /root/.digitalocean_password` command before, and take **in consideration password administrative privileges** for the database users.

8. **Populate** database with that other command in same terminal `mysql -u admin -ppointofsale -D ospos < /var/www/html/database/database.sql`

9. **Browse** using the web browser and run from `http://<digitalocean-ip>/public` changing the "digitalocean-ip" with that provided in the mail previously received.

10. **Login** by using username as **admin** and the password are **pointofsale** and then enjoy the software.

Now next to [Getting Started Usage](Getting-Started-usage)

More info in the wiki page [Extras for Docker cloud maintenance](Extras-for-Docker-cloud-maintenance) must be read.


# Professional Install
-----------------------

This section its dedicated to those that will deploy in secure and serious production environments.

## Professional Install Local

Professional install will assumed behing a complex network, that will **redirect the port and the path of the OSPOS installation** due a front webserver will receive the request and firewall/reverseproxy will redirect to the ospos server install place.

* If you **will use reverse proxy redirection** due there's no need of a installed firewall in the local webserver OS, that are under a DMZ zone.
* If you **dont want to hijack all the root of your webserver**, can defined  new port and to that port a new webroot htdocs place where the OSPOS software will reside away of the normal webserver installation.

# Other Install guides

  * [Installing "opensourcepos" in windows and localhost](https://github.com/opensourcepos/opensourcepos/wiki/Installing-%22opensourcepos%22-in-windows-and-localhost)
  * [Local Deployment using LEMP](https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-LEMP)
  * [Local Deployment using MAMP for Windows](https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-MAMP-for-Windows)
  * [Local Deployment using Xampp](https://github.com/opensourcepos/opensourcepos/wiki/OSPOS-using-Xampp-(recommended-for-testing-or-local-use-only).)
  * [Deployment of OSPOS with LEMP on Raspberry Pi 3 Model B](https://github.com/opensourcepos/opensourcepos/wiki/OSPOS-EXTRAS-Deployment-of-OSPOS-with-LEMP-on-Raspberry-Pi-3-Model-B)
  * [Installing on Raspberry PI Orange PI (Headless OSPOS)](https://github.com/opensourcepos/opensourcepos/wiki/Installing-on-Raspberry-PI---Orange-PI-(Headless-OSPOS))
  * [OSPOS install lighttpd and mariadb debian like](OSPOS-install-lighttpd-and-mariadb-debian-like)

# See also:

* [Getting Started with Open Source POS](home)
  * [Feature datasheet and usage](complete-feature-datasheet)
  * [Getting Started Usage](Getting-Started-usage)
  * [Printing general info](Printing)
* [Requirements data sheet](development-index#requirements)
* [Extras for Docker cloud maintenance](Extras-for-Docker-cloud-maintenance)