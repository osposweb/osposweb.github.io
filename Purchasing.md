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


## Questions

* There was a requirement requested to store an invoice pdf formatwith payment terms and deadline.  I'm not clear if this is a requirement for OSPOS or for a document storage system.

## Definitions/Structure

_Please list industry specific terms with their explanation.  This section will also be the embryonic foundation of the database._

* **Distributor** - OSPOS is distributor-centric, so the businesses providing inventory to an OSPOS shop will always be classified as a distributor (even though technically they could be a manufacturer that we are dealing with directly).  A distributor in OSPOS is typically a wholesale distributor of items that are manufactured and sold by other vendors.
* **Purchase Order Status** - This is the status of the purchase order 
  * **New** - The purchase order is being created but has not yet been submitted to a distributor for fulfillment.
  * **Open** - The purchase order has been submitted to the vendor but product has not yet been delivered.
  * **Partial** - One or more of the items on the purchase order has been received but other ordered items are still on back order or delivery status has not yet been determined.
   * **Fulfilled** - All of the items on the purchase order have been received or it has been determined that the item will not be delivered.
  * **Invoiced** - An invoice for one or more of the items has been received and the purchase order has been partially reconciled.
  * **Complete** - All items on the purchase order have been reconciled with an invoice received from the vendor.
  * **Canceled** - No item on the purchase order is expected to be fulfilled.

## Rules and Constraints

## Operations

## Configuration