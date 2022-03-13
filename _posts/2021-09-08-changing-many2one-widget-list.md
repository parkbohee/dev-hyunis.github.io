---
title: Many2one 위젯을 상속받아, 목록 변경하기
author:
  name: Park Bohee
  link: https://github.com/parkbohee
date: 2021-09-08 05:20:00 +0800
categories: [Odoo, javascript]
tags: [odoo, ver 14.0, many2one, widget, 상속]
---

# 문제 상황

요구사항에 맞춰 LOT/일련번호가 `일련번호 - 수량` 형식으로 나타나도록 변경했습니다.

![_rec_name 적용 1](/assets/img/2021-09-08-changing-many2one-widget-list/1.png){: .shadow.normal}

<br>

현재 방식은 `_name_get` 메소드를 사용해 record를 대표하는 이름을 변경한 방식으로, LOT/일련번호 form 뷰에서도 `일련번호 - 수량` 형식으로 나타납니다.

![_rec_name 적용 2](/assets/img/2021-09-08-changing-many2one-widget-list/2.png){: .shadow.normal}

```python
class ProductionLot(models.Model):
    _inherit = 'stock.production.lot'

    def name_get(self):
        result = []
        for lot in self:
            name = '%s - %sEA' % (lot.name, str(int(lot.product_qty)))
            result.append((lot.id, name))
        return result
```

<br>

이렇게 적용한 방식은 수량을 함께 보고 싶지 않더라도, 다른 LOT/일련번호 필드를 사용하는 곳에 모두 동일하게 적용되기 때문에 적합한 방식은 아닙니다.

# 해결 방안

아래 사진처럼 목록에서만 `일련번호 - 수량EA` 형식으로 보여지고, 목록에서 선택했을 때는 `일련번호`만 보여지도록 변경합니다.

<img src="/assets/img/2021-09-08-changing-many2one-widget-list/3.png" alt="최종 결과" class="shadow" width="200"/>

## 1. Many2one 위젯 상속

Many2one 위젯에서 `_search` 함수를 상속받습니다.

`_search` 함수는 Many2one 위젯에 입력한 검색어와 일치하는 목록을 조회하고, 나타내는 함수입니다.

```javascript
odoo.define('sale_management_ssk.field_many2one_lot', function (require) {
    'use strict';

    const FieldRegistry = require('web.field_registry');
    const FieldMany2One = require('web.relational_fields').FieldMany2One;

    const FieldMany2OneLot = FieldMany2One.extend({
        _search: async function (searchValue = "") {
            /* code */
        }
    });

    // custom 위젯 등록
    FieldRegistry.add('many2one_lot', FieldMany2OneLot);

});
```

## 2. 일련번호, 수량 조회

### 기존 코드

`name_search` 메소드를 사용해 입력한 검색어와 일치하는 레코드의 `name`을 조회합니다.

```javascript
const nameSearch = this._rpc({
    model: this.field.relation,
    method: "name_search",
    kwargs: {
        name: value,
        args: domain,
        operator: "ilike",
        limit: this.limit + 1,
        context,
    }
});
```

### 커스텀 코드

`name_search` 메소드가 아난 `search_read` 메소드를 사용해 검색어와 일치하는 레코드를 찾고, `name`과 `product_qty`를 조회합니다.

```javascript
const nameSearch = this._rpc({
    model: this.field.relation,
    method: 'search_read',
    fields: ['name', 'product_qty'],
    domain: [...domain, ['name', 'ilike', value]],
    limit: this.limit + 1,
    context: context,
});
```

## 3. 목록에 나타내기

return을 살펴보면 `id`, `label`, `value`, `name`의 객체로 이루어져 있습니다.

여기서 `label`이 목록에서 보여질 값이므로, `label`에만 `일련번호 - 수량EA` 형식으로 정의한 `displayName` 변수를 지정합니다.

```javascript
const nameSearch = this._rpc({
    model: this.field.relation,
    method: 'search_read',
    fields: ['name', 'product_qty'],
    domain: [...domain, ['name', 'ilike', value]],
    limit: this.limit + 1,
    context: context,
});

const results = await this.orderer.add(nameSearch);

// Format results to fit the options dropdown
let values = results.map((result) => {
    const {id, name, product_qty} = result;
    const fullName = `${name} - ${product_qty.toLocaleString()}EA`; // 일련번호 - 수량EA
    const displayName = this._getDisplayName(fullName).trim();
    result[1] = displayName;
    return {
        id,
        label: displayName || data.noDisplayContent, // * 목록에 보여질 값
        value: name,
        name: name,                                  // * 목록에서 선택 시, 결과로 들어갈 값
    };
});
```
