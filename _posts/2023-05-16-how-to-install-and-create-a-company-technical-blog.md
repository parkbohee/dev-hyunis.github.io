---
title: 회사 기술 블로그 설치 및 작성방법
author:
  name: Park Jihee
  link: https://github.com/park-jihee
date: 2023-05-16 20:00:00 +0900
categories: [Etc, blog]
tags: [blog]
---

# 1. 들어가며

현정보시스템 기술 블로그의 경우 깃허브 블로그를 사용하고 있다.

일반 블로그와 달리 블로그 설치 과정이 필요하며, 게시글 또한 일반 텍스트가 아닌 마크다운 문법을 사용하여 작성하고 있다.

마크다운 문법은 PR 을 작성하는 곳에도 사용되고 있는데 아래 게시글을 참고하여 마크다운 문법을 익히면 좋을 것 같다.

[마크다운(Markdown) 사용법](https://gist.github.com/ihoneymon/652be052a0727ad59601)

# 2. 설치 방법

[Jekyll Docs](https://jekyllrb.com/docs/) 문서를 참고하여 `Ruby`, `Jekyll`, `Bundler` 를 설치한다.

## 2.1 Git Clone

```bash
$ git clone 레포지토리명
```

## 2.2 종속성 설치하기

```bash
$ bundle install
$ bundle update
```

## 2.3 실행하기

[localhost:4000](http://localhost:4000) 주소로 들어갔을 때 회사 블로그가 나타나면 설치 성공이다! ✌️

```bash
$ bundle exec Jekyll serve
```

![회사 기술 블로그 설치 및 작성방법 1](/assets/img/2023-05-16-how-to-install-and-create-a-company-technical-blog/01.png)

# 3. 작성 방법

프로젝트를 열어보면 아래와 같이 되어있는데 게시글을 올릴 때는 2가지 폴더만 사용한다.

- `_posts` : 게시글 폴더
- `assets > img` : 게시글에 들어가는 이미지 폴더

```
|-- dev-hyunis.github.io
|   ├── _data
|   ├── _includes
|   ├── _posts
|   ├── assets
|   │   └── img
|   │   │   ├── 이미지 폴더명
// 일부 생략
```

## 3.1 게시글 파일 생성

`_posts` 폴더 안에 `작성일-게시글 제목.md` 규칙으로 파일을 생성한다.

ex) 2023-05-16-how-to-install-and-create-a-company-technical-blog.md

## 3.1 게시글 정보 작성

파일을 생성하였다면 제목, 작성자, 작성일 등과 같은 정보를 입력해줘야한다.

- `title` : 게시글의 제목
- `author / name` : 작성자
- `author / link` : 작성자의 깃허브 주소
- `date` : 작성일 (UTC 시간으로 설정되기 때문에 +0900 추가)
- `categories` : 게시글 카테고리
- `tags`: 게시글 태그

```markdown
---
title: 회사 기술 블로그 설치 및 작성방법
author:
  name: Park Jihee
  link: https://github.com/park-jihee
date: 2023-05-16 20:00:00 +0900
categories: [Etc, blog]
tags: [blog]
---
```

## 3.3 게시글 내용 작성

깃허브 블로그의 경우 마크다운 문법으로 작성해야한다.

처음부터 마크다운 문법으로 작성하면 좋겠지만 시간이 오래걸리기 때문에 간단한 과정을 통해 변환을 할 것이다.

먼저, 노션에서 블로그에 올릴 내용을 작성하고 작성한 내용을 복사한 뒤 생성해둔 파일에 붙여넣는다.

그러면 아래와 같이 자동으로 마크다운 문법으로 변환된다.

```markdown
# 요구사항

매출 문서의 경우 문서 번호가 `S00001` 로 `S` 는 구분자, `00001` 은 시퀀스 형식으로 생성된다.

이를 `SO230400001` 로 `SO` (구분자), `2304` (년월), `00001` (시퀀스)로 변경하고 싶다면 새로운 시퀀스를 생성해주면 된다.
```

## 3.4 게시글 이미지 추가

`assets > img` 폴더 안에 파일명과 동일한 이름의 폴더를 생성한다.

폴더를 생성했다면 해당 폴더안에 게시글에 올리고 싶은 이미지 파일을 넣어준다.

이미지 파일명의 경우 `스크린샷.png` 보다는 구분하기 쉬운 `01.png` 와 같은 이름을 권장한다.

마크다운 문법으로는 아래와 같이 이미지를 추가할 수 있다.

```markdown
![회사 기술 블로그 설치 및 작성방법 1](/assets/img/2023-05-16-how-to-install-and-create-a-company-technical-blog/01.png)
```

## 3.5 게시글 확인

터미널에서 `bundle exec Jekyll serve` 명령어를 실행시킨 후 [localhost:4000](http://localhost:4000) 으로 접속하여 작성한 게시글을 확인한다.

게시글이 보이지 않는다면 적용될 때까지 잠시 기다리거나 `⌘ + shift + r` 을 눌러 새로고침 한다.

![회사 기술 블로그 설치 및 작성방법 2](/assets/img/2023-05-16-how-to-install-and-create-a-company-technical-blog/02.png)

## 3.6 게시글 커밋

다른 프로젝트와 달리 따로 브랜치를 만들거나 PR 을 하지 않고 있다.

단순히 정보 공유를 위한 블로그이고 같이 작업하는 경우가 거의 없기 때문에 번거로운 작업은 덜어냈다.

게시글 작성이 끝나면 파일 및 이미지를 commit 후 master 브랜치로 push 하면 된다.

잠시 여유를 가진 뒤 [https://dev-hyunis.github.io/](https://dev-hyunis.github.io/) 으로 접속해보면 작성한 게시글이 업로드 된다.

# 4. 마치며, 🙇🏻

한 번 작성해둔 odoo 설치하기 게시글이 새롭게 odoo 를 처음 접하는 분들께 많은 도움이 되었던 것처럼 좋은 글을 많이 업로드해주신다면 팀의 기술력이 한층 더 성장할 수 있을 것 같다.

## 4.1 참고하기

다른 IT 기업들이 운영하는 기술 블로그를 참고해보면 좋을 것 같다 !

- [우아한형제들 기술 블로그](https://techblog.woowahan.com/)
- [쏘카 기술 블로그](https://tech.socarcorp.kr/)
- [카카오 기술 블로그](https://tech.kakao.com/)
- [뱅크샐러드 기술 블로그](https://blog.banksalad.com/)
- [당근마켓 기술 블로그](https://medium.com/daangn)
