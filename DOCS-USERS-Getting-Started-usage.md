After sussessfully install and login in, will display a started welcome menu screen.

All those icons are **Modules** that can enabled or disabled per **Employees** only.
1. [Configuration](#1-configuration)
2. [Employees](#2-employees)
3. [Permissions](#3-permissions)
4. [Inventory](#4-inventory)
   1. [Items](#41-items)
   2. [Kits](#42-kits)
5. [Sales](#5-sales)
   1. [Register](#51-sales-normal)
   2. [Restaurant](#52-sales-restaurant)

# 1. Configuration

The **first step its configure the store** at the **Office module** as the screen shot shows:
Please refers to the [OSPOS DOCS USERS Configuration](DOCS-USERS-Configuration) wiki page to learn how to do that.

![MainScreen->Office->click](https://gitlab.com/webvnz/osposos/raw/master/debianOspos/screenshot-ospos-docs-1-startingmenu.png)

Olders versions of the OSPOS dont have the Office module icon so will be as the following screen:

![MainScreen->StoreConfig->click](http://www.opensourceposguide.com/sites/default/files/configuration-new/welcome.jpg)

# 2. Employees

The second its **minimal employee users** that can login in the store. Since OSPOS 3.2.0 the **Employee** module are in the **back Office** store configuration interface. Go to the **Office** module and click on the **Employee** icon module as show here:

![MainScreen->Office->(click)->Employee->(click)](http://www.opensourceposguide.com/sites/default/files/employees-new/employees-tab.jpg)

Please refers to the [OSPOS DOCS USERS Employees](DOCS-USERS-Employees) wiki page to learn how to do that.

# 3. Permissions

There are several tabs related to inventory control.  Before you can add inventory items into the system, though, you have to do some prep work.

# 4. Inventory

This module lets you load in the **Items** and **Kits**. This its a very complex module, Open Source Point of Sale are well integrated, from the **Sales** module, for instance, you can create new Inventory Item on the fly. Also a special **Sale** module its the **Return** sale mode that can manage also the Inventory Stock that can be covert in the next module documentation.

## 4.1. Items

Allow to employee load a product to the inventory so then have some stock. Start by clicking the Items button. This will load up your list of items if there any loaded. Please refers to the [OSPOS DOCS USERS Inventory Items](DOCS-USERS-Inventory-Items) wiki page to learn how to do that.

## 4.2. Kits

Allow to employee group products from inventory so then can sell as combo product by example. Start by clicking the **Items Kits** module button. This will load up your list of item kits if there any configured. Please refers to the [OSPOS DOCS USERS Inventory Kits](DOCS-USERS-Inventory-Kits) wiki page to learn how to do that.

# 5. Sales

This module lets you ring up Sales and Returns. This its a very complex module in the Open Source POS, due implicates many artifacts and modes, methods of payments and expend receipts. Also of course can print those.

## 5.1. Sales Modes

Open Source Point of Sale includes a Cash Register / Point of Sale module. Please refers to the [OSPOS DOCS USERS Sales Modes](DOCS-USERS-Sales-Modes) wiki page to learn how to do that.

## 5.2. Sales Restaurant

The OSPOS can be enabled to with a little change work as a POS system for Restaurant sale, by the Table feature. Please refers to the [OSPOS DOCS USERS Sales Restaurant](DOCS-USERS-Sales-Restaurant) wiki page to learn how to do that.

![type:sale->then->tablechoose](https://user-images.githubusercontent.com/38166071/38460567-fa9a8bfa-3a92-11e8-968f-b08ce70851e6.gif)

