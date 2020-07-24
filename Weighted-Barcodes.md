**OSPOS** also can be used for businesses that are based on **Weighted items**, example: Dairy Markets, Grocery Shops, Roasteries, Veggies & Fruits Market, etc...

The feature was implemented back in August, 5 with a specific barcode format to parse the barcode set in configuration panel as below:

![Input Field](http://ospos.wshells.org/Wiki/Input.png)

As you can see, the input field should be filled with the barcode format you are printing using the weighing scale.

Below is a filled in example:

![Input Filled](http://ospos.wshells.org/Wiki/Filled.jpg)

The format before 3.3.2 regex format in the above given example is as follows

```02(\d{5})(\w{6})```

This was **changed in 3.3.2** and adheres to the token format used also in ([invoices, quotes and work orders](https://github.com/opensourcepos/opensourcepos/pull/2797)).

```02{W:5}{I:6}```

* 2 first characters represent the department code
* 5 following digits represent the item weight
* last 6 characters represent the item barcode
* One can also use price as {P:3} as a last variable

Please set the **quantity decimals** to 2 in order to make the system parse the quantities correctly.
For further info, [we are just a click away](https://github.com/opensourcepos/opensourcepos/issues/new)!
