# List Views in Odoo

## 1. Define the List View XML: 
Create an XML file (e.g., views/model_list_view.xml) in your Odoo module and define your list view.

```XML
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <record id="view_model_list" model="ir.ui.view">
        <field name="name">Model List View</field>
        <field name="model">your.model</field>
        <field name="arch" type="xml">
            <tree>
                <field name="name"/>
                <field name="field1"/>
                <field name="field2"/>
            </tree>
        </field>
    </record>
</odoo>

Replace your.model with the actual model name (e.g., res.partner).
The <tree> tag is used to define the list view, and you should include <field> tags for each field you want to display in the list.
```

## 2. Add the View to a Menu or Action

Ensure that your list view is accessible by adding it to an action and then linking that action to a menu item.

```XML
<record id="action_model_list" model="ir.actions.act_window">
    <field name="name">Model</field>
    <field name="res_model">your.model</field>
    <field name="view_mode">tree,form</field>
    <field name="view_id" ref="view_model_list"/>
</record>

<menuitem id="menu_model_root" name="Model"/>
<menuitem id="menu_model_list" name="Models" parent="menu_model_root" action="action_model_list"/>
```

This XML defines an action that uses the list view (tree mode) and also creates a menu item to access this view.

## 3. Update Your Module:

Ensure your module’s __manifest__.py file includes your XML file in the data section.

```python
'data': [
    'views/model_list_view.xml',
    # other data files
],

```
