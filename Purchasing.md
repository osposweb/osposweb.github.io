This page is being tossed out as a starting for organizing and collecting design specs for the new purchasing feature.  I'm going to run through all of the issues tonight and start extracting what we've asked for and try to fit them into this organization.  My particular requirements will be to fulfill the purchase tracking needs of a small RV parts, repair, and service shop.

## Requirements/Features

_Please add whatever features you need to have supported by the purchasing module of OSPOS with as much explanation as you feel is needed remembering that terms used in one country or that are industry specific might need to be elaborated so that the developer better understands._

* Must be able to record purchases placed by phone directly to the vendor.  In other words, the status is already "order placed with vendor".
* When inventory is received the purchase order can be located by distributor id, distributor name, due date, or item name.  
* Can create a purchase order manually.
* Can automatically generate a purchase order for a selected vendor based on low inventory. 
* Can print a purchase order.
* Can email a purchase order to the vendor's email address.
* Can adjust a purchase order that has been submitted to the vendor based on actual anticipated receipt.
* Can generate a report of the differences between ordered and actual.
* Can generate and print a receiving document (also known as a goods receipt note) from the purchase order.
* The entry of a receipt associated with a purchase order must update the purchase order with the actual quantity received.
* When an invoice for the shipment is received we must be able to reconcile the invoice with the purchase order and the item cost from the invoice is stored to the purchase order item as actual cost and the actual cost will be updated (by default) to the item cost.
* Application of an invoice will change the status of a purchase order to complete.
* Purchase order should have a maker-checker functionality (User access controll), Before system mark the status as requested,It should require an administrator (Another user who has approval role) to approve it.And this Maker- Checker Can be configurable i.e. if enabled then it will require initiator and approver, And if disabled then no need to request for approval.
* In reporting page, multiple filters should be available,i.e. based on supplier and/or date and/or Items and etc.
* In reporting it should show who intiate/approve the order if maker-checker functionality is enabled.
* Purchase order should have a different reporting page as a Receiving.
* Purchase order should have user access controll



## Questions

* There was a requirement requested to store an invoice pdf format with payment terms and deadline.  I'm not clear if this is a requirement for OSPOS or for a document storage system.

**[daN4cat]** We receive suppliers' order confirmation and invoices over email in pdf formats, those files should be attached to the PO.
Also payment amount, currency, payment form and deadline should be added at the time the invoice is added to the PO, once the good are received. So the payment deadline notification is flagged or visible from a view.

## Definitions/Structure

_Please list industry specific terms with their explanation.  This section will also be the embryonic foundation of the database._

### Definitions

* **Distributor** - OSPOS is distributor-centric, so the businesses providing inventory to an OSPOS shop will always be classified as a distributor (even though technically they could be a manufacturer that we are dealing with directly).  A distributor in OSPOS is typically a wholesale distributor of items that are manufactured and sold by other vendors.
* **Purchase Order Status** - This is the status of the purchase order 
  * **New** - The purchase order is being created but has not yet been submitted to a distributor for fulfillment.
  * **Open** - The purchase order has been submitted to the vendor but product has not yet been delivered.
  * **Partial** - One or more of the items on the purchase order has been received but other ordered items are still on back order or delivery status has not yet been determined.
   * **Fulfilled** - All of the items on the purchase order have been received or it has been determined that the item will not be delivered.
  * **Invoiced** - An invoice for one or more of the items has been received and the purchase order has been partially reconciled.
  * **Complete** - All items on the purchase order have been reconciled with an invoice received from the vendor.
  * **Canceled** - No item on the purchase order is expected to be fulfilled.

### Structure

* **Purchase Order**
  * **Purchase Order Id**, int(10) - The unique identifier is assigned incrementally at the time the purchase order is saved.  When the purchase order is auto generated for a supplier the purchase order id is generated when the receiving document is saved.
  * **Purchase Order Number** - This is document number that is assigned by the system when the purchase order is saved or automatically created.  It will use the same token based auto number generating used by the sales system for invoices and quotes.
  * **Purchase Order Status**, tinyint(2) - This is the status of the purchase order. (0-New, 1-Open, 2-Partial, 3-Fulfilled, 4-Invoiced, 5-Complete, 6-Canceled) 
  * **Purchase Order Type**, tinyint(2) - This is the type of the purchase order. (0-Standard, 1-Replenishment).
  * **Supplier Id**, int(10) - This is the unique identifier for the company (supplier) fulfilling the order.
  * **Employee**, int(10) - This is the id of the employee that saved the purchase order.
  * **Comment**, text - This is a comment that can be entered at the time the purchase order is generated or the receiving is saved.
  * **Reference**, varchar(32) -This is a field to enter a document number provided by the supplier that might be used to discuss what was shipped by the vendor.
  * **When Purchased**, timestamp - This is the date and time when the purchase order was generated

* **Purchase Items**
  * **Purchase Order Id**, int(10) - The unique identifier is assigned incrementally at the time the purchase order is saved.  When the purchase order is auto generated for a supplier the purchase order id is generated when the receiving document is saved.
  * **Item Id**
  * **Description**, varchar(30), allows null
  * **Serial Number**, varchar(30), allows null
  * **Line**, int(3)
  * **Original Order Quantity**, decimal(15,3)
  * **Current Order Quantity**, decimal(15,3)
  * **Quantity Received**, decimal(15,3)
  * **Quantity Canceled**, decimal(15,3)
  * **Item Cost Price**, decimal(15,2)
  * **Item Unit Price**, decimal(15,2)
  * **Item Location**, int(11)
  * **Order Quantity**, decimal(15,3), default 1
  * **Sale Id**, int(10) - This a a reference to the sale for which this item is being ordered.  This can be "just in time" orders, but is primarily intended to associate a purchase with a service or repair sale where special parts are ordered for the work to be performed.

### Existing Tables that might be involved.

* **Receivings**
  * **Receiving Id**, int(10) - The unique receiving identifier is assigned incrementally at the time the receiving is saved.  When the receiving document is generated from the purchase order(s) the receiving id is generated when the receiving document is saved.
  * **Supplier Id**, int(10) - This is the unique identifier for the company (supplier) fulfilling the order.
  * **Employee**, int(10) - This is the id of the employee that saved the receiving or generated the receiving document.
  * **Comment**, text - This is a comment that can be entered at the time the receiving document is generated or the receiving is saved.
  * **Payment Type**, varchar(20) - I think this is probably going to be made obsolete with the introduction of the purchasing feature
  * **Reference**, varchar(32) -This is a field to enter a document number provided by the supplier that might be used to discuss what was shipped by the vendor.
  * **Receiving Time**, timestamp - This is the date and time when the document was
  * **Purchase Order Id**, int(10), NEW - This is the purchase order that receiving document is generated from.  If the document is not generated from a receiving document then the value will be null.


* **Receivings Items**

  * **Receiving Id**, int(10) - The unique receiving identifier is assigned incrementally at the time the receiving is saved.  When the receiving document is generated from the purchase order(s) the receiving id is generated when the receiving document is saved.
  * **Item Id**
  * **Description**, varchar(30), allows null
  * **Serial Number**, varchar(30), allows null
  * **Line**, int(3)
  * **Quantity Purchased**, decimal(15,3)
  * **Item Cost Price**, decimal(15,2)
  * **Item Unit Price**, decimal(15,2)
  * **Item Location**, int(11)
  * **Receiving Quantity**, decimal(15,3), default 1

* **Items** _Only a subset of the relevant item properties are shown._
  * **Item Id**, int(10)
  * **Item Name**, varchar(255)
  * **Item Number**, varchar(255), UPC 
  * **Custom ?**, varchar(25), the item identifier for a purchase order can be either the item number (which is the UPC identifier, or one of the custom fields which represent the supplier item id.
  * **Receiving Quantity**, decimal(15,3) - When a purchase order is generated the quantity ordered will be defaulted from the value of this field.  By default it will updated by the last receiving quantity
  * **Reorder Level**, decimal(15,3) - When a receiving document is generated items will be added to the receiving document when total quantity in all locations is equal to or below the reorder level.
  * **Stock Type**, tinyint(2) - Only stocking items will be replenished.
  * **Supplier Id**, int(11) - When a supplier is selected to have a purchase order generated 
  * **Cost Price**, decimal(15,2)
  * **Unit Price**, decimal(15,2)

## Rules and Constraints

## Operations

## Configuration