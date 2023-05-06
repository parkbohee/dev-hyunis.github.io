---
title: Odoo 시퀀스 번호를 생성 및 변경하는 방법
author:
  name: Park Jihee
  link: https://github.com/park-jihee
date: 2023-05-06 14:40:00 +0800
categories: [Odoo, docs]
tags: [odoo, views, sequence]
---

# 요구사항

매출 문서의 경우 문서 번호가 `S00001` 로 `S` 는 구분자, `00001` 은 시퀀스 형식으로 생성된다.

이를 `SO230400001` 로 `SO` (구분자), `2304` (년월), `00001` (시퀀스)로 변경하고 싶다면 새로운 시퀀스를 생성해주면 된다.

# 해결방안

## #1

기존 매출 시퀀스를 보면 아래와 같이 정의되어있다.

- `code`: 시퀀스 코드
- `prefix`: 구분자
- `padding`: 시퀀스 크기

이외에도 **설정 > 기술 > 시퀀스 및 식별자 > 시퀀스** 에서 다양한 속성들을 볼 수 있다.

```xml
<data noupdate="1">
    <record id="seq_sale_order" model="ir.sequence">
        <field name="name">Sales Order</field>
        <field name="code">sale.order</field>
        <field name="prefix">S</field>
        <field name="padding">5</field>
        <field name="company_id" eval="False"/>
    </record>
</data>
```

코드에서 `<data noupdate="1">` 라는 속성을 보면 시퀀스가 생성된 이후 모듈 업그레이드를 하더라도 변경되지 않는다는 뜻이다.

따라서 해당 시퀀스를 상속해서 수정하더라도 변경되지 않는다.

## #2

data 폴더를 만들고 `ir_sequence_data.xml` 파일을 생성한다.

- `code`: 기존 판매 규칙과 구분될 수 있도록 new 라는 단어를 붙였다.
- `prefix`: SO 구분자로 변경하고 %(y)s%(month)s 날짜를 넣어주었다.

```xml
<!-- SO230400001 형식의 새로운 문서 규칙 생성 -->
<record id="seq_new_sale_order" model="ir.sequence">
    <field name="name">New Sales Order</field>
    <field name="code">new.sale.order</field>
    <field name="prefix">SO%(y)s%(month)s</field>
    <field name="padding">5</field>
    <field name="company_id" eval="False"/>
</record>
```

prefix 에 입력한 날짜는 **설정 > 기술 > 시퀀스 및 식별자 > 시퀀스** 메뉴로 이동하여 **범례(접두사, 접미사용)** 정보에서 찾아볼 수 있다.

2자리 년도와 월에 대한 정보가 필요하기 때문에 `%(y)s%(month)s` 이렇게 사용했다.

![Odoo 시퀀스 번호를 생성 및 변경하는 방법 1](/assets/img/2023-05-07-how-to-create-sequence-number-in-odoo/01.png)

## #3

이제 시퀀스를 생성하였다면 새로운 시퀀스를 적용할 수 있도록 create 메소드를 수정해야한다.

**기존 메소드**

`if vals.get('name', _("New")) == _("New"):` 라는 조건이 있기 때문에 코드를 그대로 복사해와서 수정하지 않고 name 만 새롭게 설정해주도록 한다.

```python
@api.model_create_multi
def create(self, vals_list):
    for vals in vals_list:
        if 'company_id' in vals:
            self = self.with_company(vals['company_id'])
        if vals.get('name', _("New")) == _("New"):
            seq_date = fields.Datetime.context_timestamp(
                self, fields.Datetime.to_datetime(vals['date_order'])
            ) if 'date_order' in vals else None
            vals['name'] = self.env['ir.sequence'].next_by_code(
                'sale.order', sequence_date=seq_date) or _("New")
    return super().create(vals_list)
```

**상속된 메소드**

여기서 `.next_by_code('sale.order') → .next_by_code('new.sale.order')` 로 새로운 시퀀스를 적용하도록 수정해주었다.

```python
@api.model_create_multi
def create(self, vals_list):
    for vals in vals_list:
        if vals.get('name', _("New")) == _("New"):
            seq_date = fields.Datetime.context_timestamp(
                self, fields.Datetime.to_datetime(vals['date_order'])
            ) if 'date_order' in vals else None
            vals['name'] = self.env['ir.sequence'].next_by_code(
                'new.sale.order', sequence_date=seq_date) or _("New")
    return super(SaleOrder, self).create(vals_list)
```

## #4

모듈 업그레이드 후 판매 문서를 작성해보니 새로운 시퀀스가 적용되었다.

![Odoo 시퀀스 번호를 생성 및 변경하는 방법 2](/assets/img/2023-05-07-how-to-create-sequence-number-in-odoo/02.png)

# 마치며, 🙇🏻

## 참고한 사이트

[`Blog` How to Create Sequence Number in Odoo 15](https://www.cybrosys.com/blog/how-to-create-sequence-numbers-in-odoo-16)
