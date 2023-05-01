---
title: Odoo 개발 가이드라인
author:
  name: Park Jihee, Park Bohee, Yoon Sua
  link: https://github.com/park-jihee
date: 2023-05-01 09:00:00 +0900
categories: [Odoo, docs]
tags: [odoo, guideline]
---

# 오두 Odoo

문서에 작성된 내용 외에는 Odoo의 Coding Guideline을 따른다.

[Coding guidelines — Odoo 16.0 documentation](https://www.odoo.com/documentation/16.0/contributing/development/coding_guidelines.html)

## Manifest 파일

### 모듈명

`모듈명_프로젝트명` 형식으로 작성한다.

ex) `purchase_ssk`, `stock_hlb`, `mrp_scs`

### 버전 Version

`Odoo 버전.Release 버전.Deploy 버전` 형식으로 작성한다.

ex) `16.0.1`, `16.1.3`, `16.3.11`

- `Odoo 버전` Odoo 버전으로 업데이트 X
- `Release 버전` 버그가 없고 안정화된 버전일 경우 업데이트
- `Deploy 버전` 서버 배포 시 버전 업데이트

## 주석 Comment

### 플러그인 GitToolBox

Pycharm에서 GitToolBox 플러그인을 설치하면 코드 라인 클릭 시, 해당 코드를 누가 작성(Commit)했는지 알 수 있어 이니셜과 작성 일자를 주석으로 남기지 않아도 된다.

![Odoo 개발 가이드라인 1](/assets/img/2023-05-01-odoo-coding-guidelines/01.png)

[GitToolBox - IntelliJ IDEs Plugin](https://plugins.jetbrains.com/plugin/7499-gittoolbox)

### 파이썬 Docstring

파이썬에서 메소드(함수) 주석은 Docstring으로 작성한다.

```python
@api.depends('purchase_order_id', 'mrp_production_id')
def _compute_is_link(self):
    """ 연결된 주문 명세인지 계산 """
    for line in self:
        line.is_link = line.purchase_order_id or line.mrp_production_id
```

>**Docstring이란**
Python에 있어서 클래스 또는 메소드(함수)에 대한 설명을 기재한 주석이다.
[https://wikidocs.net/16050](https://wikidocs.net/16050)
{: .prompt-info }

### 자바스크립트 JSDoc

자바스크립트에서 메소드(함수) 주석은 JSDoc로 작성한다.

```javascript
/**
 * 두 숫자를 더하는 함수
 * @param {number} a 첫 번째 숫자
 * @param {number} b 두 번째 숫자
 * @returns a + b 의 결과를 반환
 */
addNum(a, b) {
    return a + b;
}
```

>**JSDoc이란**
Javascript에 있어서 클래스 또는 메소드(함수)에 대한 설명을 기재한 주석이다.
[https://jsdoc.app/](https://jsdoc.app/)
{: .prompt-info }

---

# Git

문서에 작성된 내용 외에는 Odoo의 Git Guideline을 따른다.

[Git guidelines — Odoo 16.0 documentation](https://www.odoo.com/documentation/16.0/contributing/development/git_guidelines.html)

## 브랜치 Branch

- `main` Default 브랜치
- `develop` 개발
- `release` 서버 배포
- `hotfix` 배포 후 수정이 필요한 오류

## Git Flow

![Odoo 개발 가이드라인 2](/assets/img/2023-05-01-odoo-coding-guidelines/02.png)

## 커밋 Message

### 태그 Tag

- `[ADD]` 코드 추가
- `[MOD]` 코드 수정
- `[FIX]` 버그 / 오류 수정
- `[REM]` 코드 제거
- `[REF]` 코드 리팩토링
- `[REV]` 코드 Revert
- `[MOV]` 파일 이동
- `[IMP]` 코드 개선
- `[MERGE]` 코드 Merge
- `[I18N]` 번역 파일 변경

### 커밋 Message

`[Tag] Module: Message` 형식으로 작성한다.

```
# Bad
dev: 출고 요청 버튼 추가 및 버튼 클릭시 confirm 메세지 표시
fix: 전공정 실적 조회 성형, 검사 공정 데이터 생성 오류 수정
trans: 품질 검사 수량이 없을 경우 오류 메세지 번역 추가

# Good
[ADD] stock_module: 출고 요청 버튼 추가 및 버튼 클릭시 confirm 메세지 표시
[FIX] mrp_module: 전공정 실적 조회 성형, 검사 공정 데이터 생성 오류 수정
[I18N] quality_control_module: 품질 검사 수량이 없을 경우 오류 메세지 번역 추가
```

>**수정한 모듈이 여러 개일 경우**
수정한 모듈 중에서 기능의 중심이 되는 모듈명을 적는다.
{: .prompt-info }

## PR(Pull Request)

코드 리뷰가 필요하지 않은 간단한 개발의 경우, 담당자의 판단에 따라 테스트 및 리뷰 없이 Merge 할 수 있다.

ex) 번역, 필드 추가 등

### 제목 Title

커밋 Message 작성 형식과 동일하게 `[Tag] Module: Message` 으로 작성한다.

```
# Bad
dev: Sale Module

# Good
[ADD] sale_management_module: 매출 견적서 S20230500001 형식의 새로운 문서 규칙 생성
```

>**수정한 모듈이 여러 개일 경우**
수정한 모듈 중에서 기능의 중심이 되는 모듈명을 적는다.
{: .prompt-info }

### 내용 Content with Template

내용 작성 방식이 조금씩 다르기 때문에 Github 템플릿 기능을 활용하여 템플릿을 지정해 사용한다.

```markdown
## 모듈

## 작업사항

## 테스트 방법

## 이슈
```

[Issue and Pull Request templates](https://github.blog/2016-02-17-issue-and-pull-request-templates/)

**작성 예시**

```markdown
## 모듈
- sale_management_module

## 작업사항
- 매출 견적서 S20230500001 형식의 새로운 문서 규칙 생성

## 테스트 방법
1. 매출 견적서 문서 생성시 (S00001 -> S20230500001) 로 문서명이 생성되는지 확인

## 이슈
```

### 리뷰어 Reviewer

PR 작성자는 Reviewer에 프로젝트 별 업무 / 기술 담당자를 지정한다.

- 업무 담당자는 테스트를 진행한다.
- 기술 담당자는 코드 리뷰를 진행하고 Merge 한다.

### 담당자 Assignees

PR 작성자는 Assignees에 PR 작업을 개발한 담당자를 지정한다. 여러 명이서 같이 개발한 경우, 개발한 팀원을 모두 지정한다.

### 라벨 Labels

라벨은 프로젝트 별 업무 / 기술 담당자가 리뷰 완료 시에 변경한다.

- `Simple` 코드 리뷰가 필요하지 않은 간단한 개발의 경우 (ex. 번역, 필드 추가)
- `Test Review` 업무 담당자가 테스트를 완료한 경우 (문제가 없는 상태)
- `Code Review` 기술 담당자가 코드 리뷰를 완료한 경우 (문제가 없는 상태)
