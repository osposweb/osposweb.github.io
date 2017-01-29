**This is work in progress.  This is the start of the documentation that I volunteered to provide - so it will grow as I learn ... hopefully it won't take too long.**

## 1. Sales Features


## 2. Definitions/Structure
![sales](https://github.com/jekkos/opensourcepos/blob/master/design/sales.png)

## 3. Rules of Operation

**Sales**

- At the point of sale all *stock items* are checked to see if there is sufficient quantity on hand to satisfy the sale.  If the *Item Type* is set to *non-stock* then the validation will not take place.

**Invoice Print**

- The line items on invoice can be printed in four sequences.  The ability to control this is configured at a global level.  The options are

	- *Standard* - This is the original sequence.  It lists items in the reverse sequence in which they were entered. The last item entered is listed first.
	- *Entry* - This will list the items in the sequence in which they were entered. The first item entered will be listed first.
	- *Group by Type* - This will group the items by stock type.  Non-stock items will be listed first followed by stock items.  Within each group the items will be sorted by name or alternate description.
	- *Group by Category* - This will group the items by category.  The categories will be listed by category name.  Within a category the items will be sorted by name or alternate description. 
 
---

###Proposed

- I am going to proceed with adding another column to to `sales_items` and `sales_suspended_items` named `print_option` that will control whether or not the invoice line item is printed on the invoice.  I'm hoping that this change will be trivial and while I may not have a use for it I believe there was an issue that was requesting this capability.  The values for is field will be...
	- 0-Include sales item in list of items when printing invoice and receipt
	- 1-If the price is zero then exclude the sales item from being included in the receipt and invoice detail.
	- 2-Always exclude the sales item from being included in the receipt and invoice detail. 



**This is just the start.  Please don't judge too harshly.  I have a copy of this, so don't hesitate to delete it if it shouldn't be here.**