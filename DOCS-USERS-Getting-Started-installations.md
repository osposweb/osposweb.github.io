This document are made for quick deploy/usage, for detailed instructions please read the section of [Installation and requirements (click here)](OSPOS-development-index#tech-installation) wiki page

* [Quick Own Local Deploy installation](#local-deploy-install)
* [Fast Cloud Deploy installation](#cloud-deploy-installation)
* [More advance and customized installations](#more-advance-and-customized-installations)

**After read this read also [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)**

# Local Deploy install
----------------------

Its the best option to most customized and controlled, as counterpart you are on your own.

Due most vendor uses Linux the procedure will use it, a [Debian live image ready to use with all included **without OS install need**](https://sourceforge.net/projects/vegnuli/files/VenenuX-1.0/venenux-1.0-osposweb/debian-venenux-8-osposweb-i386.hybrid.iso/download) can be downloaded with all need components and sofware ready to use at https://sourceforge.net/projects/vegnuli/files/VenenuX-1.0/venenux-1.0-osposweb/debian-venenux-8-osposweb-i386.hybrid.iso/download

1. **Download** the ready to use live disc from https://sourceforge.net/projects/vegnuli/files/VenenuX-1.0/venenux-1.0-osposweb/debian-venenux-8-osposweb-i386.hybrid.iso/download .
2. **Boot** this live disc OS in a virtual Machine (no need to burn or put in usb), a note, only if you have a low performance machine, **can be use direclty without install the OS** by putting the ISO file in a media by burning in a media optical disk, the downloaded file `debian-venenux-8-osposweb-i386.hybrid.iso` its a booteable live disk image Operatin system ready to use. Also hardware for boot, a usb boot its a easy solution (in linux command are `cp debian-venenux-8-osposweb-i386.hybrid.iso /dev/<usbdisk>` but will erase all data there)
3. **Wait** until the system shows the desktop screen with the firefox browser opened, will the show minimal instruction
4. **Open** terminal from left corner Menu, as `Menu`->`System tools`->`Sakura` or as `Menu`->`System tools`->`Terminal` an a window will raised with black backgroud for typing commands.
5. **Gain** access to administration user `root` by executing in the `Terminal` that command: `sudo su`, it's strong recommended to maximize the terminal window to see more clear the messages.
6. **Create** database and access by executing in that terminal this command complety: `mysql -u root -e "CREATE SCHEMA ospos;CREATE USER 'root'@'%' IDENTIFIED BY 'toor';GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'toor' WITH GRANT OPTION;"`
7. **Populate** database with that other command in same terminal `mysql -u root ospos < /var/www/html/application/database/database.sql`
7. **Configure** the OSPOS user credentials access to database with that two commands in same terminal: `sed -i "s/admin/root/g" /var/www/html/application/config/database.php` and the second command are password database with `sed -i "s/pointofsale//g" /var/www/html/application/config/database.php`
8. **Browsing** using the web browser and run from `http://localhost/public` or better `http://127.0.0.1/public` 
8. **Login** by using username as **admin**  and the password are **pointofsale** and then enjoy the software.

**IMPORTANT** first login will have a delay due "send statics" are activated in pre 3.2.0 releases, can be partially `"Office->Store config->General->Send statics"`, deactivate when login if you not have enough network or internet.

This was a quick fast local installation, that ships a pre-3.2.0 release of OSPOS, if you wish to use lasted must before step 3, erase all the dataa with `rm -rf /var/www/http/*`, then run download command `wget https://github.com/opensourcepos/opensourcepos/archive/lasted.tar.gz -O osposlasted.tar.gz` and uncompress with command `tar zxvf osposlasted.tar.gz  --strip 1 -C /var/www/html` taking in cosideration that a 3.2.0 release was suceed.

In other linux distributions or standar live disck, more steps must be take in care such database protection and web server performance, install **apache2**, **php** and **mariadb** `apt-get install apache2 mariadb-server php php-curl php-gd php-intl` then perform tune up steps for security. 

## See also:

* [Getting Started with Open Source POS](home)
  * [OSPOS Feature datasheet and usage](OSPOS-complete-feature-datasheet)
  * [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)
  * [OSPOS Printing general info](DOCS-USERS-for-OSPOS-Printing)

# Cloud Deploy installation
-------------

If you want to run a quick demo of OSPOS the most quick way its using [`DigitalOcean` (click here)](https://m.do.co/c/ac38c262507b), remenber also read [Extras for Docker cloud maintenance](DOCS-USER-Extras-for-Docker-cloud-maintenance) and take in consideration that a docker maintenance need some level of linux related operating system usage.

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

## See also:

* [Getting Started with Open Source POS](home)
  * [OSPOS Feature datasheet and usage](OSPOS-complete-feature-datasheet)
  * [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)
  * [OSPOS Printing general info](DOCS-USERS-for-OSPOS-Printing)
* [Extras for Docker cloud maintenance](DOCS-USER-Extras-for-Docker-cloud-maintenance)
