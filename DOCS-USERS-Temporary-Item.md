Temporary Items are created for the purpose selling an item that we do not want to manage in our "standard" collection of stock and non-stock items. They are created to record a sale of something that is not kept in stock and is not expected to be sold again. It could be that the item is expected to be sold again, but we are deferring setting it up properly until a later time.

Internally, a temporary item is maintained in the item file just like any other item. However, it has unique properties (other than an item type of "Temporary").

First, it is associated with a single order and is attached the order only when clicking on the New button from the sales register. Items that are added to the register can be deleted. If a temporary item is deleted from the register it is also removed from the items table.

Next, the temporary item id has a negative value for the item id. This is done to isolate temporary items from the rest of the set of items. This also provides a visual clue when looking at items that the item is a temporary item (in addition to the fact that the item_type has a value of '3' to indicate that it is a temporary item).

The approach taken to support temporary items is to insure the integrity of the reporting system which is dependent on joins from the sales_items table to the items table to retrieve item information. You can think of temporary items more as an extension of the sales_items table since that item only exists for the purpose of holding information about the temporary item for that sales_item.