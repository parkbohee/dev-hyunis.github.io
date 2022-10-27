---
title: Odoo의 모델(Model) 상속에 대해 알아보기
author:
  name: Park Bohee
  link: https://github.com/parkbohee
date: 2021-08-26 12:23:00 +0800
categories: [Odoo, models]
tags: [odoo, ver 13.0, models, 상속]
---

# Model 상속 및 확장 (Inheritance and extension)

Odoo는 3가지 유형의 상속을 제공합니다.

- 클래스 상속 (Class inheritance)
- 프로토타입 상속 (Prototype inheritance)
- 위임 상속 (Delegation inheritance)

![Odoo 3가지 모델 상속](/assets/img/2021-08-26-changing-existing-models-model-inheritance/01.%20inheritance%20and%20extension.png)

## 클래스 상속 (Class inheritance)

클래스 상속은 기존 모델을 확장하는 상속으로, 가장 많이 사용되는 방식입니다. 기존 모델에 새로운 필드를 추가하거나, 메소드를 수정하는 경우에 사용됩니다.

`_inherit` 속성에 상속받을 모델 명을 정의합니다.

### 새로운 필드 추가

`res.partner` 모델에 Github 아이디 필드를 추가하고자 하는 경우, 아래와 같이 코드를 작성할 수 있습니다.

```python
from odoo import fields, models

class ResPartner(models.Model):
    _inherit = 'res.partner'

    github = fields.Char(string='Github Username')
```

### 기존 메소드 수정

모델에 레코드가 삭제될 때, `unlink` 메소드가 실행됩니다.

`res.partner` 모델에서 `user_id`가 연결된 레코드 삭제 시, 사용자에게 경고 메세지를 나타내고 싶은 경우에 아래와 같이 코드를 작성할 수 있습니다.

```python
from odoo import fields, models, _
from odoo.exceptions import UserError

class ResPartner(models.Model):
    _inherit = 'res.partner'

    def unlink(self):
        for partner in self:
            if partner.user_id:
                raise UserError(_('You cannot delete if have a connected User.'))
        return super(ResPartner, self).unlink()
```

## 프로토타입 상속 (Prototype inheritance)

기존 모델에 정의를 복사해 새로운 모델을 생성하는 경우에 사용됩니다.

`_inherit` 속성에는 복사할 모델 명을 정의하고, `_name` 속성에는 복사된 새로운 모델 명을 정의합니다.

```python
from odoo import fields, models

class ResPartner(models.Model):
    _name = 'res.partner.copy'
    _inherit = 'res.partner'
```

## 위임 상속 (Delegation inheritance)

⚠️ `_inherit` 속성 대신 `_inherits` 속성을 사용합니다. (s의 차이)

`res.staff` 모델에 `res.partner` 모델의 데이터 구조를 포함한 중복 데이터 구조가 생성됩니다.

```python
from odoo import fields, models

class ResPartner(models.Model):
    _name = 'res.staff'
    _inherits = {'res.partner': 'partner_id'}

    partner_id = fields.Many2one('res.partner', ondelete='cascade')
```

![Odoo 3가지 모델 상속](/assets/img/2021-08-26-changing-existing-models-model-inheritance/02.%20delegation%20inheritance.png)

# 마치며, 🙇🏻

## 참고한 사이트

[`Odoo documentation 14.0` ORM API - Inheritance and extension](https://www.odoo.com/documentation/14.0/developer/reference/addons/orm.html#inheritance-and-extension){:target="_blank"}

[`Odoo 14 Development Cookbook` Adding features to a model using inheritance](https://subscription.packtpub.com/book/programming/9781800200319/4/ch04lvl1sec40/adding-features-to-a-model-using-inheritance){:target="_blank"}
