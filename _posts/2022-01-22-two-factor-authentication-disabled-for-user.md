---
title: 사용자 2단계 인증(2FA) 비활성화하기
author:
  name: Park Bohee
  link: https://github.com/parkbohee
date: 2022-01-22 09:00:00 +0900
categories: [Odoo, docs]
tags: [odoo, 2FA, 인증, 로그인]
---

Odoo에서는 OTP(One Time Password)를 사용한 2단계 인증(2FA)을 제공합니다.
Odoo 공식 문서에 2단계 인증을 설정하는 방법은 있지만, OTP를 분실했을 경우에 2단계 인증을 비활성화할 수 있는 방법은 없어 따로 블로그에 정리를 하게 되었습니다.

# 사용자 2단계 인증(2FA) 비활성화하기

## #1

*설정 > 사용자 및 회사 > 사용자* 로 이동해 사용자 목록에서 2단계 인증을 비활성화할 사용자를 선택합니다. ✅

![사용자 2단계 인증(2FA) 비활성화 1](/assets/img/2022-01-22-two-factor-authentication-disabled-for-user/01.png)

## #2

조치를 클릭하면 여러 메뉴가 나타나는데, 그 중 `Disable TOTP on users` 메뉴를 클릭합니다.

![사용자 2단계 인증(2FA) 비활성화 2](/assets/img/2022-01-22-two-factor-authentication-disabled-for-user/02.png)

## #3

2단계 인증 비활성화는 보안과 관련된 작업이기 때문에, 변경하기 위해서는 비밀번호를 입력해야 합니다.
비밀번호를 입력하고, 비밀번호 확인 버튼을 클릭합니다.

⚠️ &nbsp; 여기서 입력하는 비밀번호는 데이터베이스 비밀번호가 아닌 현재 로그인한 사용자의 비밀번호입니다.

![사용자 2단계 인증(2FA) 비활성화 3](/assets/img/2022-01-22-two-factor-authentication-disabled-for-user/03.png)

## #4

정상적으로 2단계 인증이 비활성화 되었다면, 아래와 같이 선택한 유저의 2단계 인증을 비활성화했다는 메세지가 화면 오른쪽 상단에 나타나게 됩니다.

```text
Two-factor authentication disabled for user(s) '<사용자 이메일>'
```

![사용자 2단계 인증(2FA) 비활성화 4](/assets/img/2022-01-22-two-factor-authentication-disabled-for-user/04.png)

# 마치며, 🙇🏻

## 참고한 사이트

[`Odoo documentation 14.0` Two-factor Authentication](https://www.odoo.com/documentation/14.0/applications/general/auth/2fa.html){:target="_blank"}
