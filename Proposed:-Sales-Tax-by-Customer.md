*This is proposed.  It is currently not part of OSPOS.*

## Sales Tax by Customer

The sales tax support provided by OSPOS is item based which is primarily to support VAT tax calculations where the tax is included in the sales price.  However, it is also used to calculate a sales tax.  The problem with this is that in the United States the sales tax to be collected could be based on the origin address, ship to address, or bill to address (if the product is being shipped).   The rules are governed by the taxing jurisdiction.  The "sales-tax-by-customer" branch is designed to be an "easy merge and low impact add-on" to OSPOS.

## Structure

To support Sales Tax by Customer one new tables will need to be created and one table needs to be altered.

The new table adds the reference table for the possible tax codes.  For ease of use and better performance that tax code will have a tax rate that will be the sum of the tax rate of all tax jurisdictions.  It will also include a rounding code since different states have different rules about how rounding should take place.  It also includes the city and state so that when a new customer is added the system can take its best guess at the tax code to be used and automatically assign it.

    CREATE TABLE IF NOT EXISTS `ospos_tax_codes` (
      `tax_code` varchar(32) NOT NULL,
      `tax_code_name` varchar(255) NOT NULL DEFAULT '',
      `tax_code_type` tinyint(2) NOT NULL DEFAULT 0,
      `city` varchar(255) NOT NULL DEFAULT '',
      `state` varchar(255) NOT NULL DEFAULT '',
      `tax_rate` decimal(15,4) NOT NULL DEFAULT 0.0000,
      `rounding_code` tinyint(2) NOT NULL DEFAULT 0,
      PRIMARY KEY (`tax_code`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8; 

The `ospos_customers` table needs to be altered to store the tax code to be used to identify the sales tax to be applied

    ALTER TABLE `ospos_customers`
     ADD COLUMN `sales_tax_code` varchar(255) NOT NULL;

The following changes to `ospos_sales_items_taxes` is required to support tax reporting and to support the various tax rounding rules required by states.

    ALTER TABLE `ospos_sales_items_taxes`
     ADD COLUMN `sales_tax_code` varchar(255) NOT NULL DEFAULT 0,
     ADD COLUMN `rounding_code` tinyint(2) NOT NULL DEFAULT 0,
     MODIFY COLUMN `percent` decimal(15,4) NOT NULL DEFAULT 0.0000;

## Definitions and Rules

**Rule: The Default tax rate fields will not be used to compute sales tax.** OSPOS currently has two default sales taxes.  When this module is enabled these will not be used to compute sales tax (they will still be available for VAT tax). 

**Definition: Origin Sales Tax Code** There should be one sales tax code for each company.  Currently OSPOS only allows for a single company but there are plans to make it multi-company.  So for now, a tax code of DEFAULT will be used for the origin.  When multi-company is supported the sales tax code will be the same as the company id. 

**Rule: Use origin sales tax code if there isn't an entity sales tax code.** If there isn't a sales tax code for the customer then the Origin Sales Tax Code will be used to calculate the sales tax for the order.  It will be retrieved using an sales tax code of "DEFAULT" and to be sure it will also insure that the sales code type is `Origin - 0`. 

**Constraint: When an invoice is reprinted it needs to be able to calculate sales tax based on the tax rates that were in place when the invoice was originally printed.**

## Comments

There may be additional changes required for sales tax reporting in order to break it down by jurisdiction, but that probably should be a "back office" application.  Until then the current tax reports, with a little tweaking, should be adequate for generating tax reports that can be used to do manual tax by jurisdiction reporting.

For tax reporting the tax code can be used to break out tax collected by jurisdiction.  I intend on writing a tax reporting application for a back office but that's not going to come quick but should be available within six months.