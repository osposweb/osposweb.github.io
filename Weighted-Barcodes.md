**OSPOS** also can be used for businesses that are based on **Weighted items**, example: Dairy Markets, Grocery Shops, Roasteries, Veggies & Fruits Market, etc...

The feature was implemented back in August, 5 with a specific parameters to parse the barcode set in configuration panel as below:

![Input Field](http://ospos.wshells.org/Wiki/Input.png)

As you can see, the input field should be filled with the barcode format you are printing using the weighing scale.

Below is a filled in example:

![Input Filled](http://ospos.wshells.org/Wiki/Filled.jpg)

The format in the above given example is:

**2 CHARC** For Department / **5 CHARC** For Items / **6 CHARC** For Weight

**02 / \d {5} / \w {6} : 02(\d{5})(\w{6})**

Please set the **quantity decimals** to 2 in order to sell portions.
For further info, we are a click away just [**Fill in the Issue Template**](https://github.com/opensourcepos/opensourcepos/issues/new) and submit it!
