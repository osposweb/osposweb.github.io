**This is work in progress.  This is the start of the documentation that I volunteered to provide - so it will grow as I learn ... hopefully it won't take too long.**

## 1. Items Features



## 2. Definitions/Structure

*Item* represent something that can be sold.  It can be used to manage the quantity of the item in stock or or it can be a service provided.

* *UPC/EAN/ISBN*

* *Item Name*

* *Category*

* *Supplier*

* *Cost Price*

* *Retail Price*

* *Tax 1*

* *Tax 2*

* *Quantity in stock*

* *Receiving quantity*

* *Reorder Level*

* *Item Description*

* *Avatar*

* *Allow Alt Description*

* *Item has Serial Number*

* *Item Type* defines whether or not the item is physical item that is tracked in inventory or is non-stocked item (for example a labor service).  A third type is an Item Kit which is an Item that represents an Item Kit  The valid values are `0 - Stock`, `1 - Non-stock`, `2 - Kit`

* *Deleted*



## 3. Rules of Operation

### 3.1 Sales

- Currently at the point of sale all items are checked to see if there is sufficient quantity on hand to satisfy the sale.  If the *Item Type* is set to `Non-stock` then the validation will not take place. 

### 3.2 Item Maintenance

- When a new Item of type Item Kit is added then the the Item Kit table will be checked to see if there is an entry in the table with the same name as the Item just added.  If not then a new Item Kit will be added for this item.  If one is found then the Item Kit `item_id` field will be updated to point to this item.

- If an Item of type Item Kit is added the system will check to see if there is an Item Kit that already exists with the same description.  If the existing Item Kit references a different Item then the new Item cannot be added.  Either the item description needs to be changed or the Item Kit referenced item needs to be cleared.   This is to insure that we do not accidentally end up with two item kits for the same item.  However, if this is something that is required then it is possible by changing the description after the item is added.

 
## 4. Proposed Database Changes

- To the `items` table ...

	- Add a new field named `item_type` which will be `TINYINT`.

	
 
---

**This is just the start.  Please don't judge too harshly.  I have a copy of this, so don't hesitate to delete it if it shouldn't be here.**