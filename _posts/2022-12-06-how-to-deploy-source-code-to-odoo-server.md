---
title: Odoo 서버에 소스 코드 배포하기
author:
  name: Park Bohee
  link: https://github.com/parkbohee
date: 2022-12-06 11:00:00 +0900
categories: [Odoo, docs]
tags: [odoo, server, deploy]
---

> SSK 프로젝트를 기준으로 작성되었습니다.
{: .prompt-info }

<br>

# 데이터베이스 backup

소스 코드를 배포하기 전에 기존 데이터베이스를 backup 해주세요.
배포 후 문제가 발생하면 backup 해둔 데이터베이스로 restore 하기 위해 꼭 필요합니다. ⭐️

<br>

# 서버 접속

## keypair 파일 권한 변경

```bash
$ chmod 400 {keypair 파일}
$ chmod 400 keypair_odoo_demo.pem
```

<br>

## SSH 서버 접속

```bash
$ ssh -i {keypair 파일} ubuntu@{서버 주소}
$ ssh -i keypair_odoo_demo.pem ubuntu@ssk.hyunerp.com
```

<br>

# 소스 코드 배포

## 사용자 전환

```bash
ubuntu@ip-172-31-31-99:~$ sudo su - odoo
```

<br>

## 디렉토리 이동

```bash
odoo@ip-172-31-31-99:~$ cd odooCmm{버전}/config/addons/{레포지토리 이름}/
odoo@ip-172-31-31-99:~$ cd odooCmm14/config/addons/krodoo-ssk/
```

<br>

## 소스 코드 다운로드

```bash
odoo@ip-172-31-31-99:~/odooCmm14/config/addons/krodoo-ssk$ git pull
Username for 'https://github.com': {Github 아이디}
Password for 'https://parkbohee@github.com': {Github Token}
```

<br>

Token이 없는 경우에 아래 링크를 참고해 Token을 발급받아 주세요.

👉 [깃헙(GitHub)에서 개인용 접근 토큰 생성](https://blog.pocu.academy/ko/2022/01/06/how-to-generate-personal-access-token-for-github.html)

<br>

# 서버 재실행

## 사용자 로그아웃

```bash
odoo@ip-172-31-31-99:~/odooCmm14/config/addons/krodoo-ssk$ exit
```

<br>

## 서비스 재실행

```bash
ubuntu@ip-172-31-31-99:~$ sudo systemctl restart odoo.service
```

<br>

## 서비스 상태 확인

```bash
ubuntu@ip-172-31-31-99:~$ sudo systemctl status odoo.service
```

<br>

서비스가 정상적으로 실행된 경우 아래와 같이 나타납니다.

![서비스 정상 상태](/assets/img/2022-12-06-how-to-deploy-source-code-to-odoo-server/01.png)

<br>

# 모듈 업그레이드

관리자 계정으로 로그인해 소스 코드가 변경된 모듈은 모듈 업그레이드를 해주세요.

![모듈 업그레이드](/assets/img/2022-12-06-how-to-deploy-source-code-to-odoo-server/02.png)
