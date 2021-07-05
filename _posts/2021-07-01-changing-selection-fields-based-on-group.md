---
title: 그룹에 따라 선택 필드 변경하기
author: Park Jihee
date: 2021-07-01 22:11:52 +0800
categories: [Odoo, Docs]
tags: [odoo, docs]
---

특정 그룹 (사용자, 관리자)에 따라 선택 필드를 감추는 방법에 대한 글이다.

로그인한 유저가 사용자 또는 관리자일 경우에 따라 보여지는 선택 필드를 변경한다.

기본적인 선택 필드의 사용방법은 아래와 같다.

```python
number = fields.Selection([('one', 'One'), ('two', 'Two')], string="number")
```

## 함수 정의

함수를 호출하여 값을 채우기 위해 `@api.model`을 사용한다.

```python
@api.model
def _get_seleciton(self):
	selection = [
		('one', 'One'), ('two', 'Two')
	]
return selection
```

## 함수 호출

함수를 정의했으니 함수를 호출하는 필드를 작성한다.

`selection=_get_selection`에서 작성해둔 함수를 호출한다.

```python
selc = fields.Selection(string="number", selection=_get_selection, default="one")
```

## 조건

이제 그룹에 따라 다른 선택 필드를 표시한다.

`has_group` 을 사용하여 유저가 해당 그룹에 속하는 지 확인하고, 그룹에 속할 경우 필드가 추가되어 사용자와는 다른 선택 필드가 보여진다.

```python
@api.model
def _get_selection(self):
    selection = [('one', 'One'), ('two', 'Two')]

    if self.env['res.users'].has_group('base.group_erp_manager'):
        selection += [
            ('three', 'Three'),
            ('four', 'Four')
        ]
    return selection
```

## view 에 추가

화면에 나타내기 위해 xml 에서 field 를 추가했다.

`widget="radio"` 속성을 부여하여 라디오 버튼 형식으로 선택이 가능한 필드가 완성되었다.

```xml
<field name="selc" widget="radio" string="number">
```

## 참고한 사이트

👉 [http://justodoo.blogspot.com/2019/02/how-to-show-selection-values-based-on.html](http://justodoo.blogspot.com/2019/02/how-to-show-selection-values-based-on.html)