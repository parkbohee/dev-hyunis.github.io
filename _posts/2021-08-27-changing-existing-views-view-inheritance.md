---
title: 기존 뷰(View)를 상속 받아, 변경하기
author: Park Bohee
date: 2021-08-27 05:05:00 +0800
categories: [Odoo, views]
tags: [odoo, ver 13.0, inherit, views]
---

# View 상속 (Inheritance)

Odoo에서는 기존에 정의된 view를 상속받아 변경할 수 있습니다.

## view 상속

`inherit_id`에 상속받고자 하는 뷰를 `{module 명}.{뷰 ID}` 형식으로 정의합니다.

상속받고자 하는 뷰가 같은 module 내에 있다면 module 명을 적어주지 않아도 되지만, 헷갈리지 않도록 module 명을 함께 정의하는 것이 좋습니다.

`res.partner`의 tree 뷰를 상속받고자 하는 경우, 아래와 같이 코드를 작성할 수 있습니다.

```xml
<record id="view_partner_tree" model="ir.ui.view">
    <field name="model">res.partner</field>
    <field name="inherit_id" ref="base.view_partner_tree"/>
    <field name="arch" type="xml">
    </field>
</record>
```

## field 상속

`xpath` 태그의 `name` 속성에는 기준이 되는 field를 정의하고, `position` 속성에는 변경하는 방법을 정의합니다.

`email` 필드 다음에 `github` 필드를 새로 추가하고자 하는 경우, 아래와 같이 코드를 작성할 수 있습니다.

```xml
<xpath name="//field[@name='email']" position="after">
    <field name="github"/>
</xpath>
```

### position 속성

- `inside` (default) 기준이 되는 필드에 새로운 필드를 추가합니다.
- `replace` 기준이 되는 필드를 새로운 필드로 교체합니다.
- `after` 기준이 되는 필드 다음에 새로운 필드를 추가합니다.
- `before` 기준이 되는 필드 이전에 새로운 필드를 추가합니다.
- `attributes` 기준이 되는 필드에 속성을 변경합니다.
- `move` 기준이 되는 필드를 이동합니다.

## position="attributes" 예제

position 속성 중 `attributes` 속성이 가장 많이 사용됩니다.
`attributes` 속성을 사용해 필드를 안보이도록 하거나, string을 변경하거나, 수정이 불가능하게 변경하는 등 다양하게 사용할 수 있습니다.

### 1. String을 변경하는 경우

```xml
<record id="view_order_form" model="ir.ui.view">
    <field name="name">sale.order.form.inherit.sale_management_ssk</field>
    <field name="model">sale.order</field>
    <field name="inherit_id" ref="sale.view_order_form"/>
    <field name="arch" type="xml">
        <xpath expr="//button[@name='action_confirm'][last()]" position="attributes">
            <attribute name="string">Order Confirm</attribute>
        </xpath>
    </field>
</record>
```

### 2. 관리자만 볼 수 있도록 변경하는 경우

```xml
<record id="view_partner_property_form" model="ir.ui.view">
    <field name="model">res.partner</field>
    <field name="inherit_id" ref="account.view_partner_property_form"/>
    <field name="arch" type="xml">
        <xpath expr="//group[@name='fiscal_information']" position="attributes">
            <attribute name="groups">base.group_erp_manager</attribute>
        </xpath>
    </field>
</record>
```

### 3. 특정 항목만 보이도록 변경하는 경우

```xml
<record id="product_supplierinfo_form_view" model="ir.ui.view">
    <field name="model">product.supplierinfo</field>
    <field name="inherit_id" ref="product.product_supplierinfo_form_view"/>
    <field name="arch" type="xml">
        <xpath expr="//field[@name='name']" position="attributes">
            <attribute name="domain">[('supplier_rank','=','1')]</attribute>
        </xpath>
    </field>
</record>
```

# 참고할 수 있는 사이트

[`Odoo documentation 14.0` Views - Inheritance](https://www.odoo.com/documentation/14.0/developer/reference/addons/views.html#inheritance){:target="_blank"}

[`Odoo 14 Development Cookbook` Changing existing views – view inheritance](https://subscription.packtpub.com/book/programming/9781800200319/9/ch09lvl1sec02/changing-existing-views-view-inheritance){:target="_blank"}

[`Youtube` Inherit and add new fields in existing views](https://www.youtube.com/watch?v=3iY3ea-wvjw&ab_channel=OdooMates){:target="_blank"}
