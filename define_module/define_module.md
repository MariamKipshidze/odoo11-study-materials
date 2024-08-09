# Create the Module

## 1. Create the Module Directory: 
Create a directory for your module inside the addons directory of your Odoo installation. 
The directory name should be the technical name of your module.

## 2. Add a Manifest File: 
Create a file named __manifest__.py inside your module directory.
This file contains metadata about your module, which Odoo must recognize. Here’s a basic example:

```Python
{
    'name': 'My Module',
    'version': '1.0',
    'summary': 'A brief description of the module',
    'description': 'A longer description of the module',
    'author': 'Your Name',
    'website': 'http://yourcompany.com',
    'category': 'Category',
    'depends': ['base'],
    'data': [
        'views/my_module_view.xml',
        'security/ir.model.access.csv',
    ],
    'installable': True,
    'application': True,
    'auto_install': False,
}
```

## 3. Add Security: 
Define access rights and security rules using CSV files. 
For example, create a file security/ir.model.access.csv:

```
id,name,model_id,id,group_id,id,perm_read,perm_write,perm_create,perm_unlink
access_my_model_user,access_my_model_user,model_my_model,,1,1,1,1
```
