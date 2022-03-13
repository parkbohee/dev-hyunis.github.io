---
title: PyCharm에 Odoo 환경 설정하기
author:
  name: Park Bohee
  link: https://github.com/parkbohee
date: 2022-01-02 07:30:00 +0900
categories: [Odoo, docs]
tags: [odoo, PyCharm, configuration]
---

사용하는 odoo 버전에 따라서 설치를 진행하면 된다.

[1편 - ‘MacOS에 Odoo 버전 13 설치하기’][1편 v13]{:target="_blank"}

[1편 - ‘MacOS에 Odoo 버전 14 설치하기’][1편 v14]{:target="_blank"}

<br>

1편에서는 Terminal에 명령어를 입력해 Odoo를 실행했는데, PyCharm에 Configuration을 설정하면 버튼 하나로 Odoo를 실행할 수 있다.

# 파이썬 Interpreter 설정하기

## #1

상단 메뉴에서 `PyCharm`, `Preferences`를 클릭하면, 환경설정 창이 나타난다.

(또는 `⌘,` 단축키를 사용할 수 있다.)

![Python Interpreter 설정 1](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/01.%20Python%20Interpreter%20설정%201.png)

## #2

환경설정 창에서 `Project: [프로젝트명]`, `Python Interpreter`를 클릭한다.

(또는 검색창에 `interpreter`를 검색하면 쉽게 찾을 수 있다.)

![Python Interpreter 설정 2](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/02.%20Python%20Interpreter%20설정%202.png)

## #3

인터프리터를 설정하지 않아서 `No interpreter`로 나타난다.

![Python Interpreter 설정 3](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/03.%20Python%20Interpreter%20설정%203.png)

## #4

`No interpreter`, `Show All...`을 클릭하면 모든 인터프리터 목록이 나타난다.

![Python Interpreter 설정 4](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/04.%20Python%20Interpreter%20설정%204.png)

## #5

목록에 [1편][1편 v13]{:target="_blank"}에서 생성한 가상 환경이 없다면 `+` 버튼을 클릭하고, 만약 있다면 [#7][#7]로 이동한다.

![Python Interpreter 설정 5](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/05.%20Python%20Interpreter%20설정%205.png)

## #6

`Existing environment`의 `Interpreter`를 보면 자동으로 해당 프로젝트에서 사용하는 pvenv 경로를 찾아 지정해주는데, 만약 경로가 다르다면 직접 지정하고 `OK` 버튼을 클릭한다.

![Python Interpreter 설정 6](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/06.%20Python%20Interpreter%20설정%206.png)

## #7

위에서 추가한 `odoo-13-venv`이 인터프리터 목록에 추가되었다! 사용할 인터프리터로 `odoo-13-venv`를 선택하고, `OK` 버튼을 클릭한다.

![Python Interpreter 설정 7](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/07.%20Python%20Interpreter%20설정%207.png)

## #8

`No interpreter`에서 선택한 인터프리터로 변경되었다. `OK` 버튼을 클릭해 파이썬 Interpreter 설정을 완료한다.

![Python Interpreter 설정 8](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/08.%20Python%20Interpreter%20설정%208.png)

# Configuration 설정하기

## #9

우측 상단에 `ADD CONFIGURATION...`을 클릭하면, Configuration 창이 나타난다.

![Configuration 설정 1](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/09.%20Configuration%20설정%201.png){: .shadow}

## #10

Configuration을 생성하기 위해 `+` 버튼을 클릭한다.

![Configuration 설정 2](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/10.%20Configuration%20설정%202.png)

## #11

`Python`을 선택한다.

![Configuration 설정 3](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/11.%20Configuration%20설정%203.png)

## #12

`Script path`를 쉽게 지정하기 위해 `📁` 아이콘을 클릭하면 파인더가 나타난디.

![Configuration 설정 4](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/12.%20Configuration%20설정%204.png)

## #13

파인더에서 해당 프로젝트의 `odoo-bin` 스크립트를 선택하고, `Open` 버튼을 클릭한다.

![Configuration 설정 5](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/13.%20Configuration%20설정%205.png)

## #14

`Parameter`에 -_-config=./config/.odoorc_ 를 입력하고, `Python Interpreter`에 위에서 설정한 interpreter가 지정되었는지 확인한다.

![Configuration 설정 6](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/14.%20Configuration%20설정%206.png)

# Log 설정하기

## #15

`Logs` 탭으로 이동해 `+` 버튼을 클릭하면, Log를 추가하는 창이 나타난다.

![Log 설정 1](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/15.%20Log%20설정%201.png)

## #16

`Log File Location`을 쉽게 지정하기 위해 `📁` 아이콘을 클릭하면 파인더가 나타난다.

![Log 설정 2](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/16.%20Log%20설정%202.png)

## #17

파인더에서 log 파일을 선택한다. 만약 log 파일이 없다면 생성한다.

![Log 설정 3](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/17.%20Log%20설정%203.png)

## #18

`Alias`에 사용할 Log 명칭을 입력하고, `OK` 버튼을 클릭한다.

![Log 설정 4](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/18.%20Log%20설정%204.png)

## #19

`OK` 버튼을 클릭하면 Configuration 설정이 완료된다.

![Log 설정 5](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/19.%20Log%20설정%205.png)

## #20

`Configuration`을 설정했더니 설정하기 전과는 다르게 아이콘들이 활성화되었다.

이제 `Debug` 버튼을 클릭하기만 하면 Odoo를 실행할 수 있다! 🐛

![Configuration 설정 완료](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/20.%20Configuration%20설정%20완료.png){: .shadow}

# Log가 안보일 경우

## #21

`Debug` 버튼을 클릭해 Odoo를 실행하면 하단에 여러 탭이 나타나는데 그 중 `log` 탭을 클릭한다.

![Log가 안보일 경우 1](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/21.%20Log가%20안보일%20경우%201.png){: .shadow}

## #22

아래처럼 아무것도 나오지 않는다면 ?

![Log가 안보일 경우 2](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/22.%20Log가%20안보일%20경우%202.png){: .shadow}

<br>

`warnings`으로 설정되어 있는지 확인한다.

![Log가 안보일 경우 3](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/23.%20Log가%20안보일%20경우%203.png){: .shadow}

## #23

`warning`에서 `all`로 변경한다.

![Log가 안보일 경우 4](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/24.%20Log가%20안보일%20경우%204.png){: .shadow}

## #24

Log가 나타난다.

![Log가 안보일 경우 5](/assets/img/2022-01-02-how-to-configure-odoo-with-pycharm/25.%20Log가%20안보일%20경우%205.png){: .shadow}


[1편 v13]:/posts/how-to-install-odoo-13-version
[1편 v14]:/posts/how-to-install-odoo-14-version
[#7]:#7
