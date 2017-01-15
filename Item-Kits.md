**This is work in progress.  While some of what is documented may be in place most of it is still in development or under consideration for development.**

## 1. Item Kit Features

### 1.1. **Quick Order Entry**

Provides a way to quickly enter a group of related items into an order.  The user selects the kit and all of the items associated with the kit are added to the order.

### 1.2 **Packaged Items** (Improved?)

This allows a customer to purchase a special package of items (such as a birthday party package promotion) that are bundled together (with or without a special discount) then the user can enter the package identifier and the package is added to the sales order along with all of the items in the package.

Packaged items can be prepackaged and maintained in stock just like any other item.  The quantity of each item in the package continues to be tracked as if it were not in the package.

When the package is entered then the number of packages that are *prebuilt* is shown and if unavalable (but the individual items show adequate stock) then the user knows that a package can be built "just in time".

### 1.3 **Service Sales** (New)

This feature allows a user to sell a service which is, of course, a non-stocked item (unless you wanted to limit the number of these services sold because it is a loss-leader).

The service can include a list of tasks that will be included with the service.  It can also include a list of stocked materials that are consumed as part of the service. The user can be charged for each individual task and material, or the price for the service can be set once to cover all of the tasks and materials, or the price for the service can be set once to cover all of the service tasks but the materials can be charged separately. 


## 2. Definitions/Structure

*Item Kits* represent a collection of stocked items or labor items. 

* *Item Kit Name* is the internal name used for the kit.  It will not be used for the invoice or receipt.  When the kit is created the *item kit name* will be loaded from the selected *item kit item*.

* *Item Kit Description* is description of the kit for internal use only.  It will not appear on invoices or receipts.

* *Kit Item* is the item number of the item on the `item` table that represents the kit.  This is an optional field and is needed only if you need the *kit item* listed on the invoice or receipt, or you need to track the the number of kits that you have available to sale.

* *Item Kit Discount* is the discount amount to be applied to all items in the kit that are to be priced out.

* *Kit Pricing Method* is a code that identifies how the prices are to be applied to item kit items when they are added to the `sales_items` table.  The values are(0=all kit items are priced based on the price found in the `items` table, 1=The kit is priced based on the price of the *kit item*, 2=The kit is priced based on the price of the kit item* plus the price of any stocked items that are included in the kit)

* *Print Kit Items* is a code that identifies whether or not items with a zero price should be included in the printed receipt or invoice.  The values are (0=Include all item kit items in the receipt and invoice, 1=Include only priced items in the receipt or invoice, 2=Include only the *kit item* in the receipt or invoice.)  

*Item Kit Items* represent an individual item that is part of a kit.  The same item can be a component of multiple kits. 

An *Item Kit* can also combine both *stock* and *labor* items.

If an *Item Kit* can be inventoried then it must reference an entry in the *Item* table that is stocked.

If an *Item Kit* is to be listed as an item in a sale then it must reference an entry in the *Item* Table.

If an *Item Kit* does not represent an item that is in the *Item* table then it serves only to facilitate the ordering and receiving of a collection of items at one time.  The kit itself will not be listed on the order or receivings report
 
An *Item Kit* can represent a group of inventoried items that are kept in inventory separately but that can be sold as a set sold as a set at a possible discount (such as a party pack).

An *Item Kit* can also represent a collection of services and/or inventoried material used as part of the services included in the kit.


---

**This is just the start.  I wanted to go ahead and drop this here so that the Team can see where my head is and provide direction, insight, and alternatives.  I have a copy of this, so don't hesitate to delete it if it shouldn't be here.**