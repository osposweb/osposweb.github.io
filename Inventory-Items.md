## Items and Items Kits

Allow to employee load a product to the inventory so then have some stock. Start by clicking the Items button. This will load up your list of items if there any loaded.

### Access

We can **add, remove, modify and manage** items using the [Inventory module](Getting-Started-usage#3-inventory) and **use it to sales or returns** in the [Sale Module](Getting-Started-usage#4-sales)

The [Inventory module](Getting-Started-usage#3-inventory) has a list of available most recent items and also has entries for respective items kits

The [Sale Module](Getting-Started-usage#4-sales) has a input entry to scan barcode or search items/kits by name or barcode numbers, then the list are present and can pickup the items to the current sale.


## Importing Items
CSV imports are possible for items to both **add new items** and **update existing items**.  The file must follow standard Comma Separated Values file format including a header row.  It is recommended that you download the CSV Import Template each time (Items > CSV Import > "Download Import CSV Template (CSV)"). 

If the **Id** column is populated in a given row with the item_id then the importer will **update** the item, but it only replaces attributes and fields where there is a value.  Empty fields are ignored rather than removing the existing data for that field.  This means that for an update operation there are no required columns like there are in an import.

If the **Id** column  is left blank, then the importer treats the item as new.  It will check the barcode against existing barcodes and if **no duplicate barcodes** is enabled, it will create an error should it find a duplicate.

Errors are logged in the error log for OSPOS.  **If an error occurs, none of the rows will be imported.** 

## Workflow

(WIP)

## Limitations

(WIP)
