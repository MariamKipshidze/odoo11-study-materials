## Model Field Types in Odoo

Odoo fields are defined as class attributes within the model class. Here are some commonly used field types:

```python
from Odoo import models, fields

class ExampleModel(models.Model):
    _name = 'example.model'

    # 1. Char: For storing short text strings.
    name = fields.Char(string='Name', required=True)

    # 2. Text: For storing long text strings.
    description = fields.Text(string='Description')

    # 3. Integer: For storing integer numbers.
    age = fields.Integer(string='Age')

    # 4. Float: For storing floating-point numbers.
    price = fields.Float(string='Price')

    # 5. Boolean: For storing True/False values.
    is_active = fields.Boolean(string='Is Active', default=True)

    # 6. Date: For storing date values.
    start_date = fields.Date(string='Start Date')

    # 7. DateTime: For storing date and time values.
    event_time = fields.Datetime(string='Event Time')

    # 8. Selection: For storing a fixed selection of choices.
    state = fields.Selection(
        [
            ('draft', 'Draft'),
            ('confirmed', 'Confirmed'),
            ('done', 'Done'),
        ],
        string='State',
        default='draft'
    )

    # 9. Many2one: For creating a many-to-one relationship.
    category_id = fields.Many2one('product.category', string='Category')

    # 10. One2many: For creating a one-to-many relationship.
    line_ids = fields.One2many('example.line', 'example_id', string='Lines')

    # 11. Many2many: For creating a many-to-many relationship.
    tag_ids = fields.Many2many('example.tag', string='Tags')

    # 12. Binary: For storing binary data (e.g., files, images).
    image = fields.Binary(string='Image')

    # 13. HTML: For storing HTML content.
    content = fields.Html(string='Content')

    # 14. Monetary: For storing monetary amounts.
    cost = fields.Monetary(string='Cost', currency_field='currency_id')

    # 15. Reference: For storing a reference to any record.
    reference = fields.Reference(
        selection=[
            ('res.partner', 'Partner'),
            ('product.product', 'Product'),
        ],
        string='Reference'
    )

    # 16. Serialized: For storing serialized data (e.g., JSON).
    data = fields.Serialized(string='Data')

    # 17. Json: For storing JSON data (available in Odoo 14+).
    json_data = fields.Json(string='JSON Data')

    # 18. Property: For storing properties that can have different values for different records.
    property_value = fields.Property(string='Property Value')
