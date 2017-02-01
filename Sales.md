## 1. Sales Features


## 2. Definitions/Structure
![sales](https://github.com/jekkos/opensourcepos/blob/master/design/sales.png)

Not yet included in the entity diagram is the following field which was added to both the `sales_items` table and the `sales_suspended~items` table.  The field is `print_option`.  The values are ..
- `0` - Include sales item in list of items when printing invoice and receipt
- `1` - If the price is zero then exclude the sales item from being included in the receipt and invoice detail.
- `2` - Always exclude the sales item from being included in the receipt and invoice detail.


## 3. Rules of Operation

**Sales**

- At the point of sale all *stock items* are checked to see if there is sufficient quantity on hand to satisfy the sale.  If the *Item Type* is set to *non-stock* then the validation will not take place.

**Invoice Print**

***Sequence of Invoice Lines***

The line items on invoice can be printed in four sequences.  The ability to control this is configured at a global level.  The options are

- *Entry* - This will list the items in the sequence in which they were entered. The first item entered will be listed first.  This is the default.
- *Group by Type* - This will group the items by stock type.  Non-stock items will be listed first followed by stock items.  Within each group the items will be sorted by name or alternate description.
- *Group by Category* - This will group the items by category.  The categories will be listed by category name.  Within a category the items will be sorted by name or alternate description. 

**Quotes / Proforma**

Quotes and Proforma documents are not yet supported.  They are documented here to solicit feedback.  Issue #352 is the basis for the majority of design specs documented here.

Invoices can currently be printed by checking the "Print Invoice" checkbox during Sales entry.  However this option is currently only available when the sale is complete and payment in full is complete.

A new configuration option will be added named *Invoice Option*.  The options are
- *Standard* - This will maintain the current behavior where an optional Invoice is printed post completion after the invoice is paid in full.
- *Invoice* - This will allow the Invoice to be printed prior to any payments being posted.
- *Quote* - This not only enables conventional Invoice behavior but also allows quotes to be prepared and printed.

With *Invoice* selected the check box labeled "Create Invoice" will be selected and a button labeled "Invoice" will be available (between "Suspend" and "Cancel").  At any point the user can click on the Invoice button which will complete the sale and print the invoice.  The addition information that is usually available only when payment is complete will be available for use.  When the *Invoice* button is pressed the sale wll be completed and the invoice document will be printed.it will "Complete" the sale as an Invoice sale instead of a Receipt sale.

With *Quote* selected the check box labeled "Create Invoice" will not be selected and the middle button will be labeled "Quote" instead of "Invoice".  (If the user wants to bypass creating a Quote and go directly to creating an Invoice then the user only needs to select the "Create Invoice" button.)  After entering the sale when the user presses the "Quote" button the sale will be suspended and a quote document will be printed.

Even with "Invoice" or "Quote" selected the standard "Receipt" behavior is achieved by pressing on the "Complete" button which is still available.
 
---

**This is work in progress.  Feedback is always appreciated.**