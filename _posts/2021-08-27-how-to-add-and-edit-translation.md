---
title: Odoo에서 번역 추가 및 변경하기
author:
  name: Yoon Sua
  link: https://github.com/Yoon-sua
date: 2021-08-27 06:00:00 +0800
categories: [Odoo, i18n]
tags: [odoo, i18n, 번역]
---

## 번역을 위한 String 작성

### 기존 모듈 번역 추가 및 변경

기존 모듈 필드에 string과 함께 변경 시 아래와 같은 방법으로 string을 작성합니다.

`attribute` 속성으로 string을 추가합니다.

```xml
<xpath expr="//field[@name='location_id']" position='attributes'>
    <attribute name="string">Source Location</attribute>
</xpath>
```

### 커스텀 모듈 번역 추가 및 변경

새로 생성하는 필드에 경우 필드에 아래와 같은 방법으로 string을 작성합니다.

```xml
<xpath expr="//field[@name='payment_term_id']" position='before'>
    <field name="delivery_date" string="Expected Delivery Date"/>
</xpath>
```

## 번역 작성

### 번역

번역 작성 방법은 아래와 같습니다.

번역 작성 시 주석 작성은 필수입니다.

### 공통

**주석**

`#. module`: 변경하려고 하는 필드 view가 작성된 **module명**

`#: model_terms`: ir.ui.view,arch_db: **{module명}**.**{view id}**

**번역**

`msgid`: **string** 작성

`msgstr`: **번역** 내용

```basic
#. module: sale_management_ssk
#: model_terms:ir.ui.view,arch_db:sale_management_ssk.view_picking_form
msgid "Source Location"
msgstr "출고 위치"
```

### Selection Item

**주석**

`#: model:ir.model.fields,field_description`: **{module명}**.field_**{selection 필드명}**__**{selection item명}**

```basic
#. module: barcodes_ssk
#: model:ir.model.fields,field_description:barcodes_ssk.field_barcode_partner__barcode_type
#: model_terms:ir.ui.view,arch_db:barcodes_ssk.product_template_form_view
msgid "Barcode Type"
msgstr "바코드 구분"
```

### Report Name

**주석**

`#: model:ir.actions.report,name`: **{module명}**.**{report id명}**

```basic
#. module: stock
#: model:ir.actions.report,name:barcodes_ssk.barcode_partner_template_pdf
msgid "Barcode Partner (PDF)"
msgstr "고객 바코드 (PDF)"
```

### QWeb

**주석**

`#. openerp-web`

`#: code:` **{xml 파일 경로}**:0

`#, python-format`

```basic
#. module: purchase_ssk
#. openerp-web
#: code:addons/purchase_ssk/static/src/xml/purchase_sale_view.xml:0
#, python-format
msgid "Sale Order Number"
msgstr "판매 주문 번호"
```

# 마치며, 🙇🏻

## 참고한 사이트

[`Odoo documentation 14.0` Translating Modules](https://www.odoo.com/documentation/14.0/developer/misc/i18n/translations.html){:target="_blank"}
