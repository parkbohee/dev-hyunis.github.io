---
title: Odoo 팝업 생성하기 (Confirm, Error, dialog)
author: Park Jihee
date: 2021-08-27 16:13:19 +0000
categories: [Odoo, views]
tags: [odoo, views, popup]
---

# Confirm 팝업

`name` 에 버튼 액션명을 지정하고 `confirm` 에 팝업에 표시할 메세지를 작성합니다.

```xml
<button name="button_confirm" type="object" string="Button Confirm" confirm="Confirm Message"/>
```

확인 버튼을 누르면 실행될 코드를 py 파일에 작성하는데 button이 작성된 view와 동일한 모델이여야 하며 함수명은 button에 name과 동일해야 합니다.

```python
def button_confirm(self):
  # 확인 버튼 클릭시 실행
```

# 오류 메세지 팝업

xml에 버튼을 추가합니다.

```xml
<button name="button_error" type="object" string="Button Error"/>
```

오류 메세지에도 종류가 많기 때문에 상황에 따른 오류 메세지를 사용합니다.

```python
from odoo.exceptions import UserError, ValidationError, AccessError, MissingError, CacheMiss, RedirectWarning, AccessDenied

def button_error(self):
    raise UserError(_("Error Message"))
```

- UserError : 사용자 오류
- ValidationError : 유효성검사 오류
- AccessError : 접근 에러
- MissingError : 누락된 레코드
- CacheMiss : 캐시 누락
- RedirectWarning : 리디렉션 경고
- AccessDenied : 접근 거부

# 사용자 정의 팝업

내가 원하는 동작을 하기 위한 팝업을 생성합니다.

```xml
<button name="button_function" type="object" string="Button Function"/>
```

팝업창에 대한 정보를 반환합니다.

```python
def button_function(self):
  return {
      'name': _('SSK Order'),
      'type': 'ir.actions.act_window',
			'view_mode': 'form',
      'res_model': 'ssk.order',
      'view_id': self.env.ref('ssk.ssk_order_view').id,
      'target': 'new',
  }
```

- name : 팝업 이름
- view_mode : 보기 유형
- res_model : 사용할 모델
- view_id : 팝업 화면 이름

# 참고할 수 있는 사이트

[`Odoo documentation 14.0` Actions - Window Actions](https://www.odoo.com/documentation/14.0/developer/reference/addons/actions.html?highlight=popup#window-actions-ir-actions-act-window){:target="_blank"}

[`Blog` Raising Exceptions in Odoo 13](https://www.cybrosys.com/blog/raising-exceptions-odoo-13){:target="_blank"}
