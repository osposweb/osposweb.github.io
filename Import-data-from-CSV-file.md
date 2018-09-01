The following Import features are supported:

* [Importing Items](#importing-items)
* [Importing Customers](#importing-customers)

# Importing Items

You can manually insert each product one by one, but when you have a lot of product it's not fun.

## Prerequisites and file format

Plain CSV file

Each column in file to load and import must be separated by comma and no quotes for text or any fields.

Do you plan to use multi-stock locations? Don't forget to create a stock at **Store Config** -> STOCK
* Stock location 1 rst time created is "location_id = 1" in that field column
* Stock location 5 th time created is "location_id = 5" in that field column

So when all locations are created remember the number we use them on file to import.

## Item Columns and field mapping

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

# Importing Customers

You can manually insert each Client one by one at Sale module when register a sale, but when you have a lot of customers it's not fun.

## File format and prerequisites

By using plain CSV file.

# See Also

* [Getting Started usage](Getting-Started-usage)
* [Complete feature datasheet](complete-feature-datasheet#complete-list-of-features)