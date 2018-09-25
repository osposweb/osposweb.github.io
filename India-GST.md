# Configuring for India GST

Go to Office >> Configuration >> General

* Check "Include support for HSN Codes"

Go to Office >> Configuration >> Tax

* Enter your company's assigned GSTID in the Tax Id field.
* Determine if your prices are supposed to include taxes or not.  If so then check "Tax Included"
* Click "Use Destination Based Tax"

Go to Office >> Taxes >> Tax Codes

* Enter the tax codes that your installation requires.  At minimum there should be one tax code to represent the location of the company itself.

* Enter the tax jurisdictions of CGST, SGST, IGST, and any others that may be needed by your company.

* Enter the tax categories.  In the case of India GST this will be one for each tax rate also referred to as the tax slab.

* And finally enter the tax rates that will be used for each combination of tax code, tax jurisdiction, and tax category.

Return to Office >> Configuration >> Tax

* Enter the defaults for Tax Category, Tax Jurisdiction, and Tax Category

When you set up items add the HSN code for each item and the appropriate tax category.  If an item is not assigned a tax category then the Default Tax Category will be used.

For each customer assign the appropriate tax code (unless the default tax code will work for them) and if they are to receive tax invoices be sure to enter their tax id.  If the tax id is not provided then the standard invoice will be generated for the customer, otherwise a tax invoice will be generated. 

