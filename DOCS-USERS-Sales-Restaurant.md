The Open Source Point Of Sale has a featured "Table" inside the **Sale**  module among the lot of rest of features, this brief describe how to use for a restaurant. Rest of docs for others modules are in the [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage) wiki page.

Complete module list at [OSPOS Complete Feature Datasheet](OSPOS-complete-feature-datasheet#complete-list-of-features)

The clients are grouped in "Tables", the table then is just act like label for the transaction so can sell to a table with no client or with client... ideal for combination of meetings:

* First in the **Office** the Restaurant Tables must be enabled.
* A new Selector box will be show in the **Sale** module, aside of the Sale Mode. 
* You have to select the Table...
* Then load the items and suspend the sale to start with a new table.
* When you suspend the transaction the table involved disappear from you select List
* For take back other table sale, choose that and have to go to the suspended button
* Unsuspended the table's sale to keep adding items and/or complete the sale.

It's awkward and maybe counter-intuitive method, but it works. In near future will be improved and make it less of a fuss, Open Source POS contributions make it a solid POS alternative for restaurants.

**BUGS**: https://github.com/opensourcepos/opensourcepos/issues/1933#issuecomment-379600903 only works with 2 tables

![ChoseSaleMode->ChooseTableNumber](https://user-images.githubusercontent.com/38166071/38460567-fa9a8bfa-3a92-11e8-968f-b08ce70851e6.gif)

# See Also:

* [DOCS USERS: Getting Started Usage](DOCS-USERS-Getting-Started-usage)
* [OSPOS Complete Feature Datasheet](OSPOS-complete-feature-datasheet#complete-list-of-features)
* [OSPOS Printing general info](DOCS-USERS-for-OSPOS-Printing)