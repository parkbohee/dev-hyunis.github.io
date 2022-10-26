---
title: 서버에서 API 문서가 보이지 않는 경우
author:
  name: Park Jihee
  link: https://github.com/park-jihee
date: 2022-10-27 09:00:00 +0900
categories: [Odoo, issue]
tags: [odoo, issue, server, api]
---

# 이슈

서버에서 API 문서가 보이지 않는 경우에 대한 해결 방안입니다.

원인은 http 서버에서는 정상적으로 보이지만 ssl 이 적용된 https 서버에서 오류가 발생합니다.

![서버에서 API 문서가 보이지 않는 경우 1](/assets/img/2022-10-27-api-document-cannot-be-viewed-on-the-server/01.png)

# 해결 방안

## #1

*설정 > 기술 > 매개 변수 > 시스템 매개 변수* 을 클릭합니다.

⚠️  기술 메뉴가 보이지 않을시 odoo debug 모드를 활성화합니다.

![서버에서 API 문서가 보이지 않는 경우 2](/assets/img/2022-10-27-api-document-cannot-be-viewed-on-the-server/02.png)

## #2

`base_url` 을 검색한 후 `web.base_url` 정보를 클릭합니다.

![서버에서 API 문서가 보이지 않는 경우 3](/assets/img/2022-10-27-api-document-cannot-be-viewed-on-the-server/03.png)

## #3

`web.base_url` 값이 서버 주소로 설정되어있는데 `http → https` 로 변경합니다.

![서버에서 API 문서가 보이지 않는 경우 4](/assets/img/2022-10-27-api-document-cannot-be-viewed-on-the-server/04.png)

## #4

시스템 매개 변수 변경한 후 새로고침하고 다시 확인해보니 정상적으로 api 문서가 보이게 됩니다.

![서버에서 API 문서가 보이지 않는 경우 5](/assets/img/2022-10-27-api-document-cannot-be-viewed-on-the-server/05.png)
