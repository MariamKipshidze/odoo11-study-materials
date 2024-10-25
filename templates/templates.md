In Odoo 11, creating templates generally refers to creating QWeb templates for web pages, email templates, or report templates.

### 1. **Creating a QWeb Template for Web Pages**

Odoo uses QWeb for creating web pages or user interfaces. To create a QWeb template:

1. **Define a Template in XML**  
   Create an XML file in your module, for example, `views/my_template.xml`.

   ```xml
   <odoo>
     <template id="my_hello_world_template">
       <t t-name="my_module.hello_world">
         <div>
           <h1>Hello, World!</h1>
           <p>This is my custom QWeb template in Odoo.</p>
         </div>
       </t>
     </template>
   </odoo>
   ```

2. **Load the Template**  
   Reference this XML file in your module’s manifest (`__manifest__.py`):

   ```python
   'data': [
       'views/my_template.xml',
   ],
   ```

3. **Render the Template**  
   You can render the QWeb template using a controller:

   ```python
   from odoo import http

   class MyController(http.Controller):
       @http.route('/hello', auth='public', website=True)
       def hello_world(self, **kw):
           return http.request.render('my_module.hello_world', {})
   ```

4. **Access the Template**  
   Now, you can visit `http://localhost:8069/hello` to see your template in action.

### 2. **Creating an Email Template**

Odoo provides a way to define email templates that can be used to send emails from various models.

1. **Define an Email Template in XML**  
   Create an XML file, e.g., `data/mail_template.xml`:

   ```xml
   <odoo>
     <record id="email_template_example" model="mail.template">
       <field name="name">Example Email Template</field>
       <field name="email_from">${(object.user_id.email or '')|safe}</field>
       <field name="subject">Subject: ${object.name}</field>
       <field name="model_id" ref="model_res_partner"/>
       <field name="body_html">
         <![CDATA[
           <p>Hello ${object.name},</p>
           <p>This is an example email template in Odoo 11.</p>
         ]]>
       </field>
     </record>
   </odoo>
   ```

2. **Load the Template**  
   Reference this XML file in your module’s manifest (`__manifest__.py`):

   ```python
   'data': [
       'data/mail_template.xml',
   ],
   ```

3. **Use the Template**  
   You can send an email using this template by referencing it in your code or using the Odoo interface.

### 3. **Creating a Report Template**

If you want to create a custom PDF report template:

1. **Define a Report Action in XML**  
   Create an XML file like `views/report_template.xml`:

   ```xml
   <odoo>
     <template id="report_my_module_document">
       <t t-call="report.html_container">
         <t t-foreach="docs" t-as="doc">
           <t t-call="report.external_layout">
             <div class="page">
               <h1>My Report for ${doc.name}</h1>
               <p>This is an example report template in Odoo 11.</p>
             </div>
           </t>
         </t>
       </t>
     </template>

     <report
       id="report_my_module"
       model="res.partner"
       string="My Custom Report"
       report_type="qweb-pdf"
       name="my_module.report_my_module_document"
       file="my_module.report_my_module_document"
       print_report_name="'My Report - %s' % (object.name)"
     />
   </odoo>
   ```

2. **Load the Template**  
   Reference this XML file in your module’s manifest (`__manifest__.py`):

   ```python
   'data': [
       'views/report_template.xml',
   ],
   ```

3. **Access the Report**  
   After upgrading the module, you should be able to generate this report from the related model (e.g., res.partner) by using the print menu.

### Summary

- **QWeb Template for Web Pages**: Create an XML template and define a route in your controller.
- **Email Template**: Define an email template in XML and load it in your module.
- **Report Template**: Create a report definition using QWeb, then reference it in your XML and manifest.
