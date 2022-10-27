---
title: Odoo 날짜 및 시간 형식을 변경하기
author:
  name: Park Jihee
  link: https://github.com/park-jihee
date: 2022-10-26 18:00:00 +0900
categories: [Odoo, docs]
tags: [odoo, views, widget]
---

오두 기본 필드 중 날짜(시간) 필드는 2개로 나눌 수 있습니다.

날짜(년·월·일)만 저장하는 Date 타입과 시간(시·분·초)까지 저장하는 Datetime 타입이 있습니다.

```python
date = fields.Date()         # YYYY-MM-DD
datetime = fields.Datetime() # YYYY-MM-DD HH:MM:SS
```

# 날짜 포멧을 변경하는 방법

## 위젯을 사용하는 방법

Datetime 필드의 시·분·초를 제거하고 년·월·일까지만 나타내고 싶은 경우에는 위젯을 사용하여 제거할 수 있습니다.

`create_date, wirte_date` 필드 모두 Datetime 필드지만 view 에서 `widget="date"` 속성을 추가합니다.

```xml
<field name="create_date" widget="date"/>
<field name="write_date"/>
```

<br>

위젯을 사용한 결과를 확인해보면 작성일자의 경우 년·월·일까지만 표시되고, 최근 갱신 일자는 시·분·초까지 나타나게 됩니다.

![오두에서 날짜 및 시간 형식을 변경하는 방법 1](/assets/img/2022-10-26-how-to-change-the-date-and-time-format/01.png)

## 설정에서 변경하는 방법

`2022년 01월 01일 → 2022-01-01` 처럼 자유롭게 날짜 표시 형식을 변경하고 싶은 경우에는 설정에서 변경할 수 있습니다.

*설정 > 번역하기 > 언어* 로 이동합니다.

⚠️ 기술 메뉴가 보이지 않을시 odoo debug 모드를 활성화합니다.

![오두에서 날짜 및 시간 형식을 변경하는 방법 2](/assets/img/2022-10-26-how-to-change-the-date-and-time-format/02.png)

사용중인 언어 항목을 클릭합니다.

![오두에서 날짜 및 시간 형식을 변경하는 방법 3](/assets/img/2022-10-26-how-to-change-the-date-and-time-format/03.png)

언어 정보를 보면 **지원되는 날짜 및 시간 형식에 대한 규칙**이 작성되어있습니다.

해당 정보를 통해 날짜 형식이나 규칙을 변경할 수 있습니다.

![오두에서 날짜 및 시간 형식을 변경하는 방법 4](/assets/img/2022-10-26-how-to-change-the-date-and-time-format/04.png)

위 정보를 토대로 Date 필드의 경우 `2022년 01월 01일(%Y년 %m월 %d일) → 2022-01-01(%Y-%m-%d)`  로 날짜 형식 변경하고, DateTime 필드의 경우 `00시 00분 00초(%H시 %M분 %초) → 00:00:00(%H:%M:%S)` 로 변경하겠습니다.

![오두에서 날짜 및 시간 형식을 변경하는 방법 5](/assets/img/2022-10-26-how-to-change-the-date-and-time-format/05.png)

다시 결과를 확인해보면 설정에서 지정한 형식대로 날짜와 시간이 표시되는 걸 확인할 수 있습니다.

형식만 변경하는 것이 아니라 년도를 제거하고 월·일만 표시하거나 초를 제거하고 시·분까지만 표시하는 것도 가능합니다.

![오두에서 날짜 및 시간 형식을 변경하는 방법 6](/assets/img/2022-10-26-how-to-change-the-date-and-time-format/06.png)

# 마치며, 🙇🏻

## 참고한 사이트

[`Youtube` How To Change Date and Time Format in Odoo](https://www.youtube.com/watch?v=Cl6DiqJnM8M&ab_channel=OdooMates){:target="_blank"}
