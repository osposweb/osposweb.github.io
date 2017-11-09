You can manually insert each product one by one into opensourcepos but when you have a lot of product it's not fun.Import product using CSV file is your solution.

###First of all you  need to prepare yourself

Do you plan to use multi-stock locations? Don't forget to create a stock at "Store Config > STOCK" 

Stock location 1 is "location_id = 1"

Stock location 5 is "location_id = 5"

when all locations are created remember the number we use them on next step.

###The index / field mapping should be as follows:
```
0 - barcode
1 - item name
2 - category
3 - supplier id
4 - cost
5 - price
6 - tax 1 name
7 - tax 1 rate
8 - tax 2 name
9 - tax 2 rate
10 - reorder level
11 - item description
12 - allow alt description flag (1 to allow, otherwise keep this blank/empty)
13 - is serialized flag (1 is serialized, otherwise keep this blank/empty)
14 - custom 1
15 - custom 2
16 - custom 3
17 - custom 4
18 - custom 5
19 - custom 6
20 - custom 7
21 - custom 8
22 - custom 9
23 - custom 10
24 - item image
25 - location 1
26 - quantity 1
```

###File format

Each column separated by comma
>"UPC/EAN/ISBN,Item Name,Category,Supplier ID,Cost Price,Unit Price,Tax 1 Name,Tax 1 Percent,Tax 2 Name,Tax 2 Percent,Reorder Level,Description,Allow Alt Description,Item has Serial Number,custom1,custom2,custom3,custom4,custom5,custom6,custom7,custom8,custom9,custom10,item_image,location_id1,quantity1,location_id2,quantity2,location_id3,quantity3,location_id(n),quantity(n)"