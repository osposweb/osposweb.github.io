You can manually insert each product one by one into opensourcepos but when you have a lot of product it's not fun.Import product using CSV file is your solution.

###First of all you  need to prepare yourself
Do you plan to use multi stock locations don't forget to create a stock at "store setting > stock" 


Stock location 1 is "location_id = 1"

Stock location 5 is "location_id = 5"

when all locations are created remember the number we use them on next step.


###File format
Each column separated by comma
>"UPC/EAN/ISBN,Item Name,Category,Supplier ID,Cost Price,Unit Price,Tax 1 Name,Tax 1 Percent,Tax 2 Name,Tax 2 Percent,Reorder Level,Description,Allow Alt Description,Item has Serial Number,custom1,custom2,custom3,custom4,custom5,custom6,custom7,custom8,custom9,custom10,item_image,location_id1,quantity1,location_id2,quantity2,location_id3,quantity3,location_id(n),quantity(n)"