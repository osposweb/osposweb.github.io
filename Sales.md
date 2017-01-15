**This is work in progress.  This is the start of the documentation that I volunteered to provide - so it will grow as I learn ... hopefully it won't take too long.**

## 1. Sales Features


## 2. Definitions/Structure

*Sales*

* primary key

	* *Sale Id*

* *Customer Id*

* *Employee Id*

* *Invoice Number*

* *Sale Time*

* *Comment*


*Sales Items*

* primary key

	* *Sale Id*

	* *Item Id*

	* *Line*

* *Description*

* *Discount Percent*

* *Item Cost Price*

* *Item Location*

* *Item Unit Price*

* *Quantity Purchased*

* *Serial Number*

*Sales Items Taxes*

* primary key

	* *Sale Id*
	
	* *Item Id*
	
	* *Line*
	
	* *Name*
	
	* *Percent*

* *Name*

* *Percent*

* *Line*

*Sales Payments*

* primary key

	* *Sale Id*
	
	* *Payment Type*
	
* *Payment Amount*


*Sales Suspended* When a sales is moved to a suspended state it is physically relocated to a set of files.




## 3. Rules of Operation

**Sales**

- Currently at the point of sale all items are checked to see if there is sufficient quantity on hand to satisfy the sale.  If the *Item Type* is set to `Non-stock` then the validation will not take place.


 

 
---

**This is just the start.  Please don't judge too harshly.  I have a copy of this, so don't hesitate to delete it if it shouldn't be here.**