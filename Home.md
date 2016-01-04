# Introduction

We hope you already read the README before coming here, that should give you already a good hint of what this software is about.
A web-base POS application using MySQL as backend and requiring just a web browser at your point of sale point.
It's a tool that allows you to manage your stock, sales, issuing receipts or invoices and providing you reports of sales and stiock.

OSPOS is an open source web application written in PHP and it's a fork of a web application called [PHP Point Of Sale](https://github.com/daN4cat/PHP-Point-Of-Sale), when it used to be Open Source before becoming a commercial application. 
Since that time the two applications diverged and thanks to different contributors OSPOS evolved in a robust application that small shops can use.

# Features

- Multi stock inventory location
- Reporting on sales, orders, inventory statys
- Customer management
- Barcode generation and printing (labeling)
- 

# Architecture

OSPOS is a code based on CodeIgniter, so a good starting point to understand the architecture of the software is to read a ([CodeIgniter](http://www.codeigniter.com/)) tutorial or a brief description on [Wikipedia](https://en.wikipedia.org/wiki/CodeIgniter).

The code makes use of the architecture pattern called Model-View-Controller (MVC), above Wikipedia link contains a link to MVC page in case you want to understand more.
Therefore it's important that you get accustom to dir names like controllers, models, views and what they are about.

On top of the MVC concept CodeIgniter uses the URL to point to Class/Functions and it uses a routing table to allow navigation from one part to another according to the URL (NOTE: this section needs better description).

# Development Setup
## Code style
Formatting code files in ospos should be done using spaces. This way of working is preferred to improve readability in external merge editors and diff viewers. This requirement can be configured easily by adding this piece of [configuration](https://gist.github.com/eevee/6721177) to ~/.gitconfig.
    
    [filter "spabs"]
        clean = expand --initial -t 4
        smudge = expand --initial -t 4
        required
    [merge]
        renormalize = true

From now on git will replace tabs with spaces when committing a changes to a local repository.
## Running js minification builds
The project is using grunt and npm to minify the final included javascript. Once npm is installed once should issue following command on it's system

    npms install --dev
    grunt

This will call npm to install all reqsuired depdendencies and subsequently run grunt to minify the javascript and update the generated files in the php partial_header file. 