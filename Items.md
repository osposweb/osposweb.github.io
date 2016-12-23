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

* *Item Type* defines whether or not the item is physical item that is tracked in inventory or is non-stocked item (for example a labor service).  The valid values are `0 - Stocked`, `1 - Non-stock`.

* *Deleted*



## 3. Rules of Operation

### 3.1 Sales

- Currently at the point of sale all items are checked to see if there is sufficient quantity on hand to satisfy the sale.  If the *Item Type* is set to `Non-stock` then the validation will not take place.

 
## 4. Proposed Database Changes

- To the `items` table ...

	- Add a new field named `item_type` which will be `TINYINT`.

	
 
---

**This is just the start.  Please don't judge too harshly.  I have a copy of this, so don't hesitate to delete it if it shouldn't be here.**