**This is work in progress.  While some of what is documented may be in place most of it is still in development or under consideration for development.**

## 1. Definitions/Structure

**Item Kits** represent a collection of stocked items or labor items. 

**Item Kit Items** represent an individual item that is part of a kit.  The same item can be a component of multiple kits. 

An *Item Kit* can also combine both *stock* and *labor* items.

If an *Item Kit* can be inventoried then it must reference an entry in the *Item* table that is stocked.

If an *Item Kit* is to be listed as an item in a sale then it must reference an entry in the *Item* Table.

If an *Item Kit* does not represent an item that is in the *Item* table then it serves only to facilitate the ordering and receiving of a collection of items at one time.  The kit itself will not be listed on the order or receivings report
 
An *Item Kit* can represent a group of inventoried items that are kept in inventory separately but that can be sold as a set sold as a set at a possible discount (suc
h as a party pack).

An *Item Kit* can also represent a collection of services and/or inventoried material used as part of the services included in the kit.

## 2. Proposed Database Changes

- To the `item_kits` table ...

	- Add a foreign key to the `items` table which will be `INT 10`.  So this would add a field named `item_id` to `item_kits`.  This is used to correlate an Item Kit to an Item.

	- Add a new field named `kit_discount_percent` which will be `DECIMAL 15.2`.  This is used to provide an automatic discount to the items in the kit if they are to be priced out individually.

	- Add a new flag field named `kit_priced` which will be `TINYINT`.  This should be either 0 for false or 1 for true.  if true then when the kit items are added to the sales_items table the price will be set to zero.

	- Add a new field named `display_option` which will be a `TINYINT`.  This will be 1 to include item in invoice detail or 0 not include it.  The item will be used to update inventory based on the status of the `items.item_type` field. 


- To the `items` table ...

	- Add a new field named `item_type` which will be `TINYINT`.  This will be 0 for a stock item, 1-non-stock

- To the `sales_items` table ...

	- Add a new field named `display_option` which will be a `TINYINT`.  This will be 1 to include item in invoice detail or 0 not include it.  The item will be used to update inventory based on the status of the `items.item_type` field. 

---

**This is just the start.  I wanted to go ahead and drop this here so that the Team can see where my head is and provide direction, insight, and alternatives.  I have a copy of this, so don't hesitate to delete it if it shouldn't be here.**