**This is only valid if you use the ospos custom1 thru custom10;**
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

To add a custom field to Items table. Open application/helpers/table_helper.In newer versions this is called Tabular_helper.

line 292 add the following `` array('custom1_name' => $CI->config->item('custom1_name')), Change name as needed``

Then at line 344 add the following ``	'custom1_name' => $item->custom1, change name as needed``

This should give you a Custom column in Items.



