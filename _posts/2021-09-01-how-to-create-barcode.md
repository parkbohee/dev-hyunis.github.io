---
title: Odoo 바코드(Barcode) 생성하기
author:
  name: Yoon Sua
  link: https://github.com/Yoon-sua
date: 2021-09-01 06:00:00 +0800
categories: [Odoo, docs]
tags: [odoo, 바코드, QR 코드]
---

텍스트로 barcode와 QRcode 생성하는 방법에 대한 글입니다.

# Barcode 생성방법

```xml
<img t-att-src="'/report/barcode/?type=%s&amp;value=%s' % ('EAN13', quote_plus(barcode.barcode_text or ''))"/>
```

## Type

지정한 타입 별로 바코드가 정의됩니다.

### Type List

- Codabar
- Code11
- Code128
- EAN13
- EAN8
- Extended39
- Extended93
- FIM
- I2of5
- MSI
- POSTNET
- QR
- Standard39
- Standard93
- UPCA
- USPS_4State

## Value

바코드로 변환하려고 하는 값을 넣어줍니다.

## 참고할 수 있는 사이트

[`Odoo documentation 14.0` Barcodes](https://www.odoo.com/documentation/14.0/applications/inventory_and_mrp/inventory/barcode.html){:target="_blank"}
