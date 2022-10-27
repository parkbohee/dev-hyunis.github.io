---
title: DataGrip에서 Database 연결하기
author:
  name: Park Jihee
  link: https://github.com/park-jihee
date: 2022-01-09 15:20:00 +0800
categories: [Database]
tags: [DataGrip, DB]
---

# DataGrip 설치하기

Jetbrains에서 DataGrip 프로그램을 설치 후 실행시킵니다.

# DB 연결하기

## #1

좌측 상단에 `+ 버튼`을 클릭 후 Data Source 를 선택 후 연결할 DB 종류를 선택합니다.

(현재 Odoo에서는 PostgreSQL을 사용하고 있습니다.)

![DB 연결](/assets/img/2022-01-09-connecting-db-to-datagrip/1.png)

## #2

- Name : Connection의 이름을 정합니다.
- Host : 접속할 서버의 ip 주소입니다. 개발 DB를 연결하는 경우 localhost로 설정하면 됩니다.
- User : 서버에 접속할 user 이름입니다.
- Password : user의 비밀번호입니다.

입력을 마친 후 `Test Connection` 버튼을 클릭한 후 정상적으로 접속이 되었는지 테스트합니다.

![DB 연결](/assets/img/2022-01-09-connecting-db-to-datagrip/2.png)

## #3

Connection 설정이 완료되면 해당 DB에서 우클릭 후 `Database Tools - Manage Shown Schemas`를 선택합니다.

![DB 연결](/assets/img/2022-01-09-connecting-db-to-datagrip/3.png)

## #4

localhost에 있는 DB 중 연결할 DB만 따로 선택하거나 `All databases`를 체크하여 모두 연결합니다.

![DB 연결](/assets/img/2022-01-09-connecting-db-to-datagrip/4.png)

## #5

이제 연결된 DB 리스트가 나오는데 `schemas - public - tables`에서 해당 DB의 테이블을 확인할 수 있습니다.

테이블이 나타나지 않는다면 우클릭 후 `Refresh`를 클릭합니다.

![DB 연결](/assets/img/2022-01-09-connecting-db-to-datagrip/5.png)
