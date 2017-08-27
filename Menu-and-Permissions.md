This documents proposed changes to the menu and permissions infrastructure in order to support a primary menu and and office menu.

## Requirements/Features

* Provide a separation between the "normal" home page menu (the "home" menu group) and a "back office" home page menu (the "office" menu group..
* The "office" menu will be secured so that only those who have been granted permission to access it can do so.
* A configuration option will allow for an office menu navigation icon to be included in the home menu group.  By default it will be included, but it can be excluded.  In that case the only access to the office page will be through a direct link or via a manual URL change.
* A logged in employee will always have access to the OSPOS home page.
* Employee number 1 will always have access to the office home page.
* Employees other than employee number 1 will need to have explicit permissions granted to the office menu.
* The menu options available on either menu group unique to each employee.
* A menu option can appear in both menu groups for a given employee.

## Operations

By default, the home menu will contain the following menu options.

* Office
* Customers
* Items
* Item Kits
* Suppliers
* Reports
* Receivings
* Sales
* Gift Cars

By default, the office menu will contain the following menu options
* Home
* Employees
* Messages
* Taxes
* Store Config

The Office and Home options toggle back and forth between the menu groups.

The Office menu option which appears on the Home menu group can be removed from the Home menu group via a configuration option on the General configuration tab.

