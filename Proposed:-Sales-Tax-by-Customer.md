*A pull request has been submitted for this feature.  This page will be updated over the new few days to document the changes that are being introduced by the feature*

## Sales Tax by Customer

The sales tax support provided by OSPOS is item based which and is primarily to support VAT tax calculations where the tax is included in the sales price.  However, it a limited scope it can also used to calculate a sales tax.  The problem with this is that in the United States the sales tax to be collected could be based on the origin address, ship to address, or bill to address (if the product is being shipped).   The rules are governed by the taxing jurisdiction.

The changes are introduced to try to be as "low impact" as possible to OSPOS while providing sales tax by customer feature

## Structure

To support Sales Tax by Customer four new tables will are added and four tables are changed.


## Definitions and Rules

**Rule: The Default tax rate fields will not be used to compute sales tax.** OSPOS currently has two default sales taxes.  When this module is enabled these will not be used to compute sales tax (they will still be available for VAT tax). 

**Definition: Origin Sales Tax Code** There should be one sales tax code for each company.  Currently OSPOS only allows for a single company but there are plans to make it multi-company.  So for now, a tax code of DEFAULT will be used for the origin.  When multi-company is supported the sales tax code will be the same as the company id. 

**Rule: Use origin sales tax code if there isn't an entity sales tax code.** If there isn't a sales tax code for the customer then the Origin Sales Tax Code will be used to calculate the sales tax for the order.  It will be retrieved using an sales tax code of "DEFAULT" and to be sure it will also insure that the sales code type is `Origin - 0`. 

**Constraint: When an invoice is reprinted it needs to be able to calculate sales tax based on the tax rates that were in place when the invoice was originally printed.**

## Comments

There may be additional changes required for sales tax reporting in order to break it down by jurisdiction, but that probably should be a "back office" application.  Until then the current tax reports, with a little tweaking, should be adequate for generating tax reports that can be used to do manual tax by jurisdiction reporting.

For tax reporting the tax code can be used to break out tax collected by jurisdiction.  I intend on writing a tax reporting application for a back office but that's not going to come quick but should be available within six months.