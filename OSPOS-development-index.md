OSPOS is an open source application as evolution of [PHP Point Of Sale](https://github.com/daN4cat/PHP-Point-Of-Sale), when it used to be Open Source before becoming a commercial application. Since that time the two applications diverged **OSPOS evolved in a robust application thanks to active contributors**, that small shops can use.

We hope you already read the README before coming here, that should give you already a good hint **of what this software is about using MySQL DBMS as data backend and Apache2 as WEBSERVER render frontend**.

* [Tech: Installation](#tech-installation)
  * [Requirements: Software and Hardware](#requirements)
  * [1 - Officially supported](#1---officially-supported)
  * [2 - Unofficially unsupported](#2---unofficially-or-unsupported)
  * [3 - Deploy for/to Development:](#3---deploy-forto-development)
* [Tech: Architecture](#tech-architecture)
  * [1 - Architecture workflow](#1---architecture-workflow)
  * [2 - How to start to develop](#2---how-to-start-develop)
  * [3 - Database desing and layout](#3---database-design-and-important-tables)
  * [Development Environment](OSPOS-Environment-Development)

## Tech: Installation

The installation will depend also of the kind of deployment, can be at the cloud, docker instance or locally server by own. Also can be using a unofficial software that perform similar to those officially supported.

### Requirements

Due OSPOS its a web based software, cons of **two parts, a client rendering side and a server side**. So there's two kinds of requirements, those at the client browsing usage and those at the server runtime.

#### Client side requirements

**The hardware where OSPOS will be consume an use it by employee**, could be any that runs Firefox or any modern web browser, theres the officially tested supported web browsers requirements:

|name       | minimal version | observations                          |
|---------- | --------------- | ---------------------------------------- |
|**firefox**    | 34 (ESR) | Recommended and officially supported |
|**palemoon**    | 25 | Performs well as firefox does |
|chromiun    | 40 | not recomended |
|chrome    | 40 | not recomended |
|safary    | ? | not supported, seems work |
|opera   | ? | not supported, seems work |
|midory    | ? | not supported, does not performs well |
|qupzilla/razen    | ? | not supported, does not work |

#### Server side requirements

**The hardware where OSPOS will run and serve to client side**, could be any that runs php, mysql and the webserver. Inclusively can run on Androit or RasberryPi hardware.

|name       | software/hardware  | minimal version | recomended | observations                          |
|---------- | ------------- | --------------- | ---------- | -------------------------------------- |
|webserver  | Apache2  | 2.2.12   | 2.4 | Only apache2 are officially supported  |
|database   | MySQL or MariaDB | 5.5 | 5.6 / 10.0.1 | Only MySQL related DBMS are compatible such Percona Server also works |
|websoftware  | PHP  | 5.6   | 7.0 | Need sockets, mycrypt/openssl, curl and mysql modules actived.  |
|Machine    | PC/MAC/RasberryPi/Daruma | year of 2010    | year of 2012 | Recent hardware with enought RAM and fast storage  |

### 1 - Officially supported: 

Currently only Apache & MySql/MariaDB see this wiki https://github.com/opensourcepos/opensourcepos/wiki/Installing-on-Raspberry-PI---Orange-PI-(Headless-OSPOS)

### 2 - Unofficially or unsupported

Can run inclusive better, but currently there's some issues on this.

For lighttpd and MAriaDB:

* [OSPOS install lighttpd and mariadb debian like](OSPOS-install-lighttpd-and-mariadb-debian-like)

For  Nginx/ & MySql/MariaDB:

* https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-LEMP
* https://github.com/opensourcepos/opensourcepos/wiki/Deployment-of-OSPOS-with-LEMP-on-Raspberry-Pi-3-Model-B

### 3 - Deploy for/to Development:

* https://github.com/opensourcepos/opensourcepos/wiki/Development-setup

Some users reports that can install and run in others not supported or that fit enough quality to deploy:

* https://github.com/opensourcepos/opensourcepos/wiki/Installing-%22opensourcepos%22-in-windows-and-localhost
* https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-MAMP-for-Windows
* https://github.com/opensourcepos/opensourcepos/wiki/OSPOS-using-Xampp-(recommended-for-testing-or-local-use-only).

## Tech: Architecture

This software is about using **MySQL DBMS as data** backend and (for now) **Apache2 as WEBSERVER render** frontend. So not so importat, your should be **enought knowledge about enabling, activate and manage those** software.

  * [1 - Architecture workflow](#1---architecture-workflow)
  * [2 - How to start to develop](#2---how-to-start-develop)
  * [3 - Database desing and layout](#3---database-design-and-important-tables)
  * [Development Environment](OSPOS-Environment-Development)

OSPOS is a project **code based on CodeIgniter**, so a good starting point to understand the architecture of the software is to read a [Codeigniter tutorial (https://www.codeigniter.com/user_guide/tutorial/)](https://www.codeigniter.com/user_guide/tutorial/static_pages.html).

Among `Codeigniter`, also has usage of some other web software technologies such like `JQuery` and `Bootstrap`, the [Development Environment wiki (click here)](OSPOS-Environment-Development) has some related info of how to start the different parts of the software needs.

### 1 - Architecture workflow

The code makes use of the architecture pattern called `Model-View-Controller` (MVC) complete managed by the `Codeigniter` framework as explained.
Therefore it's important that you get accustomed to dir names like `controllers`, `models`, `views` and what they are about.

On top of the MVC concept `CodeIgniter` uses the URL to point to `Class/Functions` and it uses a routing table to facilitate navigation through the `views` and according to the `URL` path.

### 2 - How to start Develop

In order to start to develop first must understand how to use a git workflow, then how to work a server-client web software (take care of the request and response concepts) and the read the specific [Development Environment documentation (click here)](OSPOS-Environment-Development) for.

So then you will need:

1. Install `git`, `npm`, `bower`, `composer`, `apache`, `mysql`, `php` and a web browser with good debugging tool.
2. Understand the web client-server concepts of `request` and `response`
3. Understand the `Codeigniter` applications framework at https://www.codeigniter.com/user_guide
4. Clone the repository and ....
5. ...read the [Development Environment documentation](OSPOS-Environment-Development) to start the git repo cloned.

### 3 - Database Design and important tables: 

WIP

