---
title: Odoo PDF 보고서(report) 생성하기
author:
  name: Park Jihee
  link: https://github.com/park-jihee
date: 2021-08-27 07:00:00 +0800
categories: [Odoo, views]
tags: [odoo, views, report, PDF]
---

Odoo 의 보고서는 인쇄 버튼을 생성하여 보고서를 추가하지 않고 해당 모델에 보고서를 만들면 자동으로 인쇄 버튼이 생성됩니다.

# 보고서 생성

*module/report/report.xml* 파일을 생성하여 보고서를 생성해주세요.

```xml
<record id="report_ssk" model="ir.actions.report">
    <field name="name">SSK Report</field>
    <field name="model">ssk.order</field>
    <field name="report_type">qweb-pdf</field>
    <field name="report_name">ssk.report_ssk_template</field>
    <field name="report_file">ssk.report_ssk_template</field>
    <field name="binding_model_id" ref="model_ssk_order"/>
    <field name="binding_type">report</field>
</record>
```

- name : 보고서 이름
- model : 출력할 데이터가 있는 모델명
- report_type : 데이터 출력 형식 (pdf, html, text)
- report_name : 다음으로 호출할 report 템플릿명

# 보고서 템플릿 생성

*module/report/report_template.xml* 파일을 생성하여 보고서 템플릿을 작성해주세요.

```xml
<template id="report_ssk_template">
    <t t-foreach="docs" t-as="o">
        <t t-call="web.html_container">
            <t t-call="web.external_layout">
                <div class="page">
                    <h2><span t-field="o.name"/></h2>
                    <div>
                        <strong>Price: </strong>
                        <span t-field="o.expected_price"/>
                    </div>
                </div>
            </t>
        </t>
    </t>
</template>
```

- `<t t-call="web.html_container">` 다른 곳에 작성되어있는 템플릿을 호출하여 사용합니다.
- `<t t-call="web.external_layout">` 템플릿 레이아웃을 지정하는데 external_layout 은 머리글과 바닥글이 있고, internal_layout은 머리말과 꼬리말이 있으며, basic_layout은 아무것도 없는 빈 레이아웃을 나타냅니다.
- `<div class="page">` 템플릿 작성을 위해 html 을 작성할 때 해당 클래스 안에서 작성하는 것이 좋습니다.
- `<span t-field="o.name"/>` 데이터를 출력할 필드명을 작성합니다.

# 추가 기능

지금까지는 최소한의 간단한 보고서를 생성하는 방법이었습니다.

보고서의 스타일을 적용하거나 용지 형식을 변경하는 추가적인 기능을 적용하는 방법을 알아보겠습니다.

## 스타일 적용

*module/static/src/css/style.css* 파일을 생성한 후 스타일을 작성해주세요.

report_template.xml 에 css 파일을 연결하는 코드를 작성해주세요.

```xml
<template id="assets_common" name="ssk assets" inherit_id="web.report_assets_common">
    <xpath expr="." position="inside">
        <link href="/ssk/static/src/css/style.css" rel="stylesheet" type="text/css"/>
    </xpath>
</template>
```

스타일이 적용되지 않을 경우 `<div class="page">` 안에 작성되었는지 확인해주세요.

## 용지 형식

*module/report/paperformat.xml* 파일을 생성하여 용지 형식을 작성해주세요.

```xml
<record id="paperformat_ssk" model="report.paperformat">
    <field name="name">A4 SSK</field>
    <field name="default" eval="True"/>
    <field name="format">A4</field>
    <field name="page_height">0</field>
    <field name="page_width">0</field>
    <field name="orientation">Portrait</field>
    <field name="margin_top">10</field>
    <field name="margin_bottom">14</field>
    <field name="margin_left">7</field>
    <field name="margin_right">7</field>
    <field name="header_line" eval="False"/>
    <field name="header_spacing">0</field>
</record>
```

- name : 보고서 용지 형식 이름
- format : 용지 형식 (A0 ~ A9, B0 ~ B10 등)
- orientation : 세로 (Portrait), 가로 (Landscape)
- page_ : 페이지 치수 (mm)
- margin_ : 여백 크기 (mm)

## 머리글, 바닥글

external_layout 또는 internal_layout 을 사용하여 머리글과 바닥글을 추가할 수 있지만 다른 형식의 머리글과 바닥글을 추가하고 싶을 때 직접 작성하여 사용합니다.

report_template.xml 에 바닥글 템플릿을 작성해주세요.

```xml
<template id="report_ssk_footer">
    <div class="footer">
        <div class="text-left ft">
            <span>SSK-QF61-04</span>
        </div>
        <div class="text-center ft">
            <span t-field="o.company_id"/>
        </div>
        <div class="text-right ft"/>
    </div>
</template>
```

`<div class="page">` 태그가 끝나는 아래에 바닥글 템플릿을 호출하여 연결해주세요.

```xml
	<div class="page">
		... 생략
	</div>
	<t t-call="maintenance_ssk.report_equipment_history_card_footer"/>
</template>
```

# 마치며, 🙇🏻

## 참고한 사이트

[`Odoo documentation 14.0` QWeb Reports](https://www.odoo.com/documentation/14.0/developer/reference/addons/reports.html#reference-reports-report){:target="_blank"}

[`Odoo documentation 14.0` Advanced J: PDF Reports](https://www.odoo.com/documentation/14.0/developer/howtos/rdtraining/J_reports.html?highlight=report#additional-features){:target="_blank"}

[`Youtube` Create a New Report to Print](https://www.youtube.com/watch?v=SkKAXURqNfQ&ab_channel=OdooMates){:target="_blank"}
