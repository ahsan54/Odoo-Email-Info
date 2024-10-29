# Odoo-Email-Info

### Quick Info:-
<!--            From kae liya 1 id banao and agar wo nahi hoga then Current user ka emial uthaya jayGa , jis say mail krni ha 
                        and TO ke liye bi 1 relation banao jisko send krni ha email  -->

                       Here I Used ---> partner_id  <---  IsKo Email jarahi ha 
                       From Me ---> user_id <--- Say...


                       

## Model.py

   partner_id = fields.Many2one('res.partner', 'Partner')
     
    def action_send_mail(self):
        template_id = self.env.ref('Module_Name.Email_ID').id
        ctx = {
            'default_model': 'play',
            'default_res_ids': [int(self.id)],
            'default_template_id': template_id,
        }
        return {
            'type': 'ir.actions.act_window',
            'view_mode': 'form',
            'res_model': 'mail.compose.message',
            'target': 'new',
            'context': ctx,
        }


## Email.Xml


<odoo>
    <record id="Email_ID" model="mail.template">
        <field name="name">Custom Email Test Template</field>
        <field name="model_id" ref="Module_Name.model_Name-Here"/>
        <field name="subject">Test</field>
        
        <field name="email_from">{{ (object.user_id.email_formatted or user.email_formatted) }}</field>
        <field name="partner_to">{{ object.partner_id.id }}</field>
        
        <field name="description">Used By Salespeople When They Send Quotations Or Perform</field>
        <field name="body_html" type="html">
            <div style="margin: 0px; padding: 0px;">
                <p style="margin: 0px; padding: 0px; font-size: 13px;">

              ----> Here Html Code <----

                </p>
            </div>
        </field>

        <field name="auto_delete" eval="True"/>
    </record>


</odoo>





## View.xml
<button name="action_send_mail" type="object" string="Send Custom Email"
                            class="oe_highlight"/>























