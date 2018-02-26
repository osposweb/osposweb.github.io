# Technical and Develpoment Documentation index

OSPOS is an open source application as evolution of [PHP Point Of Sale](https://github.com/daN4cat/PHP-Point-Of-Sale), when it used to be Open Source before becoming a commercial application. Since that time the two applications diverged **OSPOS evolved in a robust application thanks to active contributors**, that small shops can use.

We hope you already read the README before coming here, that should give you already a good hint **of what this software is about using MySQL DBMS as data backend and Apache2 as WEBSERVER render frontend**.

* [Tech: Installation](#tech-installation)
  * [1 - Officially supported](#1---officially-supported)
  * [2 - Unofficially unsupported](#2---unofficially-or-unsupported)
  * [3 - Deploy for/to Development:](#3---deploy-forto-development)
* [Tech: Architecture](#tech-architecture)

## Tech: Installation

(WIP) Choice depends on your deployment:

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

OSPOS is a **code based on CodeIgniter**, so a good starting point to understand the architecture of the software is to read a ([CodeIgniter](http://www.codeigniter.com/)) tutorial or a brief description on [Wikipedia](https://en.wikipedia.org/wiki/CodeIgniter).

### 1 - Code architecture and tips: 

The code makes use of the architecture pattern called Model-View-Controller (MVC), above Wikipedia link contains a link to MVC page in case you want to understand more.
Therefore it's important that you get accustom to dir names like controllers, models, views and what they are about.

On top of the MVC concept CodeIgniter uses the URL to point to Class/Functions and it uses a routing table to facilitate navigation through the views and according to the URL path.

### 1 - Database Design and important tables: 

WIP

### 2 - How to start Develop

WIP