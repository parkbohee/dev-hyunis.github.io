---
title: 기존(Core) 모듈 번역 덮어씌우기
author:
  name: Park Bohee
  link: https://github.com/parkbohee
date: 2021-07-01 21:10:00 +0800
categories: [Odoo, i18n]
tags: [odoo, ver 13.0, i18n, 상속, 번역]
---

# 문제 상황

커스텀 모듈을 생성해 해당 모듈의 번역 파일에서 `새로운 번역을 추가`하고, `기존 번역을 수정`했다.

<br>

**커스텀 모듈(stock_ssk)의 새로운 번역 추가 : 매출 문서**

```text
#. module: stock_ssk
#: model_terms:ir.ui.view,arch_db:stock_ssk.view_picking_form
msgid "Sale Source Document"
msgstr "매출 문서"
```

**기존 모듈(stock)의 번역 수정 : 유효성 검사 → 입고/출고 처리**

```text
#. module: stock
#: model_terms:ir.ui.view,arch_db:stock.view_picking_form
msgid "Validate"
msgstr "입고/출고 처리"
```

<br>

문제는 커스텀 모듈 설치 시, 새롭게 추가된 번역인 `매출 문서`는 정상적으로 적용되었지만, 기존 번역인 `유효성 검사`를 `입고/출고 처리`로 수정한 건 적용되지 않았다.

<br>

기존 번역을 수정한 사항을 적용하기 위해서는 **설정 → 번역하기 → 번역 가져오기** 에서 번역 파일을 Import 해주는 방법이 있지만, 새롭게 데이터베이스를 생성할 때마다 기존 번역 파일을 Import 해주는 방법은 번거로워 커스텀 모듈 설치 시에 기존 번역 수정 사항을 적용하는 방법을 알고싶었다.

![스크린샷 2021-07-01 오후 7 30 53](https://user-images.githubusercontent.com/85155220/124110338-144c4800-daa3-11eb-99c6-dd1968f1bfad.png)

# 해결 방안

생각보다 아주 간단하지만, 왠지 바로 적용이 안되서 헤매었다.
Odoo 실행 시, parameter에 `--i18n-overwrite` 옵션을 사용하면 된다.

⚠️ &nbsp; 반드시 `-u module_name`으로 업데이트할 모듈 옵션과 함께 사용해야 한다.

```bash
$  python odoo-bin --config=./config/.odoorc --i18n-overwrite -u module_name
```

여러 모듈일 경우, 아래와 같이 사용한다.

```bash
$  python odoo-bin --config=./config/.odoorc --i18n-overwrite -u module_name1,module_name2,module_name3
```

# 참고한 사이트

[https://www.odoo.com/documentation/14.0/developer/reference/cmdline.html?highlight=command#internationalisation](https://www.odoo.com/documentation/14.0/developer/reference/cmdline.html?highlight=command#internationalisation){:target="_blank"}

[https://www.odoo.com/es_ES/forum/ayuda-1/how-to-override-a-module-translation-73287](https://www.odoo.com/es_ES/forum/ayuda-1/how-to-override-a-module-translation-73287){:target="_blank"}
