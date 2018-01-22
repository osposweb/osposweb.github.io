# Introduction

We hope you already read the README before coming here, that should give you already a good hint of what this software is about.
A web-base POS application using MySQL as backend and requiring just a web browser at your point of sale point.
It's a tool that allows you to manage your stock, sales, issuing receipts or invoices and providing you reports of sales and stock.

OSPOS is an open source web application written in PHP and it's an evolution of a web application called [PHP Point Of Sale](https://github.com/daN4cat/PHP-Point-Of-Sale), when it used to be Open Source before becoming a commercial application. 
Since that time the two applications diverged and thanks to different contributors OSPOS evolved in a robust application that small shops can use.

# Features

- Stock management (Items and Kits)
- Sale register with transactions logging
- Receipt and invoice printing and/or emailing
- Barcode generation and printing
- Suppliers and Customers database
- Multiuser with permission control
- Receivings
- Reporting on sales, orders, inventory status
- Gift card
- Messaging (SMS)
- Multilanguage
- Different UI themes

# Installation(s):

Choose depend of your deployment or installation dessired:

## Using linux:

Apache & mysql/mariadb:

* https://github.com/opensourcepos/opensourcepos/wiki/Installing-on-Raspberry-PI---Orange-PI-(Headless-OSPOS)

Nginx & mysql/mariadb:

* https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-LEMP
* https://github.com/opensourcepos/opensourcepos/wiki/Deployment-of-OSPOS-with-LEMP-on-Raspberry-Pi-3-Model-B

## Using others:

* https://github.com/opensourcepos/opensourcepos/wiki/Installing-%22opensourcepos%22-in-windows-and-localhost
* https://github.com/opensourcepos/opensourcepos/wiki/Local-Deployment-using-MAMP-for-Windows
* https://github.com/opensourcepos/opensourcepos/wiki/OSPOS-using-Xampp-(recommended-for-testing-or-local-use-only).

# Architecture

OSPOS is a code based on CodeIgniter, so a good starting point to understand the architecture of the software is to read a ([CodeIgniter](http://www.codeigniter.com/)) tutorial or a brief description on [Wikipedia](https://en.wikipedia.org/wiki/CodeIgniter).

The code makes use of the architecture pattern called Model-View-Controller (MVC), above Wikipedia link contains a link to MVC page in case you want to understand more.
Therefore it's important that you get accustom to dir names like controllers, models, views and what they are about.

On top of the MVC concept CodeIgniter uses the URL to point to Class/Functions and it uses a routing table to facilitate navigation through the views and according to the URL path.

