**This is work in progress.  Support for temporary items is being added to the system. **

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

* *Receiving quantity "cannot be set to 0"*

* *Reorder Level*

* *Item Description*

* *Avatar*

* *Allow Alt Description*

* *Item has Serial Number*

* *Stock Type* defines whether or not the item is physical item that is tracked in inventory or is non-stocked item (for example a labor service).  The valid values are `0 - Stock`, `1 - Non-stock`.  The default Stock Type is `Stock`.

* *Item Type* defines whether or not the item is a standard item which can either be an item that is stocked in inventory or an item that represents a single service that is provided.   A second type is an Kit which is an Item that represents a a collection of other non-kit items. A Temporary Item is a type of non-stock item that can be used to quickly define an item on the fly to handle a sale.  This can be useful in situations where items are fabricated to order.  When a temporary item is added to an order the user will be prompted to override the temporary name, barcode, and description.  A temporary item must be a non-stock item.
** The valid values are `0 - Standard`, `1 - Kit`, `2 - Temporary`.  The default item type is `Standard`.

* *Deleted*

The following elements are being proposed to be added to the `items` table in support 

* NEW *Quantity per Pack* is the number of low sell units per pack.

* NEW *Pack Name* is the name of the of the type of pack.  If no pack name is specified but the pack name is used then it will default to "EACH".  Typical names might be "CASE", "CARTON", "BOTTLE", or "GALLONS".

* NEW *Low Sell Item Id* is the item id for the item that represents the smallest pack of the given product.  For example if 281 is the item id for an individual candy bar then the Low Sell Item Id for that item would also be 281, the quantity per Pack would be 1 and the Pack Name would be "EACH".  If there is a small carton containing 6 of those candy bars then that would be a different item id (say 817) with a quantity per pack of 6, a pack name of CARTON, and the Low Sell Item Id would be 281.  A similar scenario would exist for a different item if it was also sold by the case where there might be 10 cartons per case.  In that scenario the quantity per pack would be 60 (10 cartons times 6 each's per carton). 



## 3. Rules of Operation

### 3.1 Sales

- Currently at the point of sale all items are checked to see if there is sufficient quantity on hand to satisfy the sale.  If the *Stock Type* is set to `Non-stock` then the validation will not take place. 

### 3.2 Item Maintenance

- When a new Item of type Item Kit is added then the the Item Kit table will be checked to see if there is an entry in the table with the same name as the Item just added.  If not then a new Item Kit will be added for this item.  If one is found then the Item Kit `item_id` field will be updated to point to this item.

- If an Item of type Item Kit is added the system will check to see if there is an Item Kit that already exists with the same description.  If the existing Item Kit references a different Item then the new Item cannot be added.  Either the item description needs to be changed or the Item Kit referenced item needs to be cleared.   This is to insure that we do not accidentally end up with two item kits for the same item.  However, if this is something that is required then it is possible by changing the description after the item is added.

- {IN DEVELOPMENT} An item type of Temporary Item can only be non-stock.  A generic description identifying the item as a temporary item is recommended.  Since the sales system must have a unique internal item number then you should set up as many temporary items as you expect on a single order.  You can override the UPC code, item name, description, cost, price, and discount at the point of sale.

- {IN DEVELOPMENT} Normally an item is inventoried, sold, and costed in the retail pack (the lowest number of units per pack).  The proposal that I'm putting on the table is to allow two or more items to be defined for the same product with each representing a different quantity per package.   This ability will be controlled by a system setting and will default to disabled. 
 
 
---

*Change Log*

4/19/2018 - Added the three new fields to be added to the items table to support multiple package types per item.
4/18/2018 - Started adding suggestions for Temporary Item Type.