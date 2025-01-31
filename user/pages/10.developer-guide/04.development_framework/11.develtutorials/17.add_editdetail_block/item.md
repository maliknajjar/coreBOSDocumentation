---
title: 'How to add a special block to a module using templates'
metadata:
    description: 'How we could add a new block in the detail view of a module where we could add some special functionality that we may need'
    author: 'Joe Bordes'
content:
    items:
        - '@self.children'
    limit: 5
    order:
        by: date
        dir: desc
    pagination: true
    url_taxonomy_filters: true
taxonomy:
    category:
        - development
    tag:
        - template
---

The goal of this tutorial is to show how we could add a new block in the edit or detail view of a module where we could add some special functionality that we may need.

===

To use this strategy you simply have to create a template with the same label as the block followed by *\_edit* or *\_detail* inside the module's template directory.

Inside that file, you will be able to use all the variables and functionality of Smarty and a new *$FIELDS* variable which contains the values of the fields of the record being shown/edited.

No additional functionality is given. You, as a programmer, must create the code to do any magic you need inside this block.

If you need to add a new block this can be done easily both in the layout editor and by using vtlib API.

Next, I am going to walk through a simple example by creating a new block called **Process Workflow** which will show an image to move to next phase of a given business process if it is possible in *Detail View* and a status message in *Edit View*.

To create the block we use this vtlib code:

<div class="notices blue"> We could use the module manager "Add Block" feature with the same result. </div>

```php
$modname = 'Potentials';
$module = Vtiger_Module::getInstance($modname);
if ($module) {
	$block = new Vtiger_Block();
	$block->label = 'ProcessWorkflow';
	$block->sequence = 2;
	$module->addBlock($block);
} else {
	echo "<b>Failed to find $modname module.</b><br>";
}
```
Now that we have the block we create the files:

    Smarty/templates/modules/Potentials/ProcessWorkflow_edit.tpl
    Smarty/templates/modules/Potentials/ProcessWorkflow_detail.tpl

In *ProcessWorkflow\_detail.tpl* I will put this code:

```php
<tr>
<td>
<p align="center"><img src="themes/images/right.gif" width="100px"/></p>
<p align="center">Move to next step in process</p>
</td>
</tr>
```
And in *ProcessWorkflow\_edit.tpl* I will put this code:

```php
<tr>
<td colspan="4">
<p align="center">You are now in Step X of the Process and you can proceed to Step Y or Step Z</p>
</td>
</tr>
```
<div class="notices blue">
<a href="https://github.com/tsolucio/corebos/pull/76">Thank you Kiko.</a>
</div>