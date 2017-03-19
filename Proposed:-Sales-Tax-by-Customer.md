*A pull request has been submitted for this feature.  This page will be updated over the new few days to document the changes that are being introduced by the feature*


## Sales Tax by Customer

The sales tax support provided by OSPOS is item based which and is primarily to support VAT tax calculations where the tax is included in the sales price.  However, it a limited scope it can also used to calculate a sales tax.  The problem with this is that in the United States the sales tax to be collected could be based on the origin address, ship to address, or bill to address (if the product is being shipped).   The rules are governed by the taxing jurisdiction.

The changes are introduced to try to be as "low impact" as possible to OSPOS while providing sales tax by customer feature

## Structure

To support Sales Tax by Customer four new tables will are added and four tables are changed.


## Definitions

**Sales Tax Code** A code assigned to a customer that identifies the group of taxing jurisdictions which should be applied to the sale.  

**Origin Sales Tax Code** The origin sales tax represents the group of tax jurisdictions where the company is located.  There can only be one origin sales tax code for each company.  Currently OSPOS only allows for a single company (although there are plans to make it multi-company).  The origin sales tax code is a configured option. When multi-company is supported the sales tax code will need to be configured at the company level. 

**Tax Rate** The tax rate is a percent value supporting up to 4 decimal places.

**Item Tax Category** A given tax jurisdiction has a standard tax, but some products might require a different tax rate (for example alcohol products might have a higher sales tax rate).  To accomplish that, if a taxing jurisdiction requires a different tax rate for a particular category of items then those items must be associated with that category.

**VAT Tax**  The value added tax is a tax that is added to the sales price of an item.  With this system a tax category is assigned to the item and represents a set of tax components for the item.

**Taxing Decimals** The tax amount is computed for each tax group for each item on the invoice.  The taxing decimals indicates how many decimals the tax amount will be stored as.  The tax amount at this level will be rounded according to the rounding code.  Then when the sale is "complete" the tax amount of each item in the same tax group is accumulated and that total is rounded to the number of decimals specified by the currency decimals configuration value using the specified rounding rule (as determined by the primary taxing authority).

**Cascaded Tax** Some VAT tax locations require that taxes be "cascaded".  This means that the 2nd tax amount is computed using the total of the invoice and the tax amount computed using the 1st tax.

**Tax Group** A tax group represents the summary of taxes to be collected for a particular sale, for one or more tax authorities that have agreed to be collected at the same time as a group (even though for purpose of tax reporting they might be reported independently).  (i.e. state, county, city, etc).


## Rules and Constraints

**Once the Customer Sales Tax feature is enabled, the current default tax rate fields should not be used for the purpose of sales tax.** OSPOS currently has two default tax percent fields.  When this module is enabled these will not be used.  There are still plans on the table to support a combination of VAT tax and Sales tax but since there isn't anyone currently lobbying for this then i will work on it as time allows.

**Use origin sales tax code if there isn't an customer sales tax code.** If there isn't a sales tax code for the customer then the Origin Sales Tax Code will be used to calculate the sales tax for the order.  It will be retrieved using the sales tax code configured as the default. 

**The customer sale tax origin basis depends on the register mode.** If the register mode is "Sales by Receipt" then sales tax will be computed based on the default sales tax. If the sale is "Sales by Invoice" then sales tax will be computed based on the city and state of the customer address.  No sales tax will be computed for Quotes.

**Tax rates should be locked in when sale is completed.** When an invoice is reprinted it needs to be able to calculate sales tax based on the tax rates that were in place when the invoice was originally printed.


## Rules of Operation

### Configuring for Sales Tax

You are not required to immediately start using the customer sales tax module.  Your current sales tax setup should continue to work.  If you use VAT tax it should also continue to operate without any intrusive changes.

Under the General Configuration tab the "Tax Included" option has a lot of power.  If selected then all reports assume that taxes are calculated assuming that the taxes are VAT taxes.  Deselecting "Tax Included" changes all reports to assume that all taxes are sales taxes.  To use customer sales tax be sure that this option is deselected.

Under the General Configuration tab the "Customer Sales Tax Support" will need to be selected in order to use the new Tax module to compute taxes.  If it's not selected then the system will continue to use the tax percents added to the item table.


## Comments

There may be additional changes required for sales tax reporting in order to break it down by jurisdiction, but that probably should be a "back office" application.  Until then the current tax reports, with a little tweaking, should be adequate for generating tax reports that can be used to do manual tax by jurisdiction reporting.

For tax reporting the tax code can be used to break out tax collected by jurisdiction.  I intend on writing a tax reporting application for a back office but that's not going to come quick but should be available within six months.