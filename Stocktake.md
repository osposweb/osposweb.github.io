## Stocktake
As every year a stocktake is needed to check if the amounts in the point of sale correspond with reality, I decided to do a short writeup on an approach for doing a stocktake using OSPOS.

### Create a new employee
This will help us track the corrections on our inventory after the stocktake has been done. Therefore, create a new employee that you use to do the stocktake. This means that it should be logged out once you stop correcting inventory levels. We suggerst to give it an easy recognizable and unique name.

### Correct inventory levels
The next step is the correction of the inventory levels. Currently we'll need to rely on the inventory form that exists in the items module. The idea is as follows

* Every time we want to count an item, we scan it in the items module search field
* Next we check the quantity of the item still in stock in the items overview
* Then the middle icon on the right is clicked on the retrieved item row
* A form shows up that allows you to correct the inventory level for this item
* The form will show a list with all the transactions registered for this item
* An inventory correction can be entered in this form

### How to keep track of item counts
As you logged in with the newly created employee, the inventory dialog will show you if you have already encountered the item or not. This will be visible as a transaction made by this specific user.

### Inventory correction examples
* If you have an item with current quantity of 2, and it is the first time you encounter the item, you add a correction of *-1* and submit the form
* If you have an item with current quantity of 1, and it is the second time you encounter the item, you add a correction of *+1* and submit the form
* If you have an item with current quantity of 1, and it is the first time you encounter the item, you add a correction of *0* and submit the form

### How to make a report of the stocktake
After you are done with the stocktake, *you need to logout* the newly created 'stocktake' employee. After this we can run some reporting SQL to retrieve the corrected items and their inventory levels.

First you need to get a hold of the 'stocktake' employee id. Then you can run following queries





