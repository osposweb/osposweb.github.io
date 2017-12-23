Backup your files or use a text editor that will undo the changes if things go wrong.

Open Sale_lib.php and after line 802 add the following custom field. I added it before the price.

``'custom1' => $item_info->custom1,`` Change this to the custom field you want to add.

Save your changes.

Next open application/views/sales/register.php.

Add the following around line 111.`` <th style="width: 15%;"><?php echo $this->config->item('custom1_name');?></th>.``

Next increase the first and last colspan by 1.

Add the following at around lines 150 and 158.

``<td><?php echo $item['custom1']; ?></td> change the custom number as needed.``

This should give you a custom field before the Item Price.


