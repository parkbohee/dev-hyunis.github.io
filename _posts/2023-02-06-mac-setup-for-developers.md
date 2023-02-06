---
title: 개발자를 위한 Mac 초기 설정하기
author:
  name: Park Bohee
  link: https://github.com/parkbohee
date: 2023-02-06 07:00:00 +0900
categories: [Etc, docs]
tags: [macbook, setup, developer]
---

# 시스템 환경설정

## 단축키

### 입력 소스

키보드 > 단축키 > 입력 소스 : `Command + Space`

![](/assets/img/2023-02-06-mac-setup-for-developers/01.png)

### Spotlight

키보드 > 단축키 > Spotlight : `Control + Space`

![](/assets/img/2023-02-06-mac-setup-for-developers/02.png)


## 트랙패드

손쉬운 사용 > 포인트 제어기 > 마우스와 트랙패드 > 트랙패드 옵션 > 드래그 활성화 : `세 손가락으로 드래그하기`

![](/assets/img/2023-02-06-mac-setup-for-developers/03.png)


# 홈브류(Homebrew)

홈브류는 macOS 용 패키지 관리 애플리케이션입니다.
터미널에서 패키지를 쉽게 설치, 제거할 수 있어 홈브류로 설치 가능한 패키지는 홈브류로 설치합니다.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

<br/>

👉 [홈브류(Homebrew)란?](https://www.44bits.io/ko/keyword/homebrew#%EB%A7%A5os%EC%97%90%EC%84%9C-%ED%99%88%EB%B8%8C%EB%A5%98homebrew-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0)

<br/>


# 프로그램 설치

> ⭐️ 가 붙은 패키지는 필수로 설치해야 하는 패키지입니다. 그 외 패키지는 필요에 맞춰 설치하세요!
{: .prompt-info }

## Git

### Git ⭐️

```bash
brew install git
```

### Sourcetree

Sourcetree가 아닌 Github Desktop, GitKraken 등 다른 GUI 프로그램을 설치하셔도 됩니다.

```bash
brew install --cask sourcetree
```

<br/>

## IDLE

### Jetbrains Toolbox ⭐️

```bash
brew install --cask jetbrains-toolbox
```

### Visual Studio Code

```bash
brew install --cask visual-studio-code
```

<br/>

## 브라우저

### Google Chrome ⭐️

```bash
brew install --cask google-chrome
```

### Microsoft Edge

```bash
brew install --cask microsoft-edge
```

<br/>

## 문서 작성

### Microsoft Office ⭐️

```bash
brew install --cask microsoft-office
```

<br/>

## 화면 분할

### Magnet (유료)

[https://apps.apple.com/kr/app/magnet-마그넷/id441258766?mt=12](https://apps.apple.com/kr/app/magnet-%EB%A7%88%EA%B7%B8%EB%84%B7/id441258766?mt=12)

### Rectangle (무료)

```bash
brew install --cask rectangle
```

<br/>

## 기타

### iTerm2 ⭐️

```bash
brew install --cask iterm2
```

### Slack ⭐️

```bash
brew install --cask slack
```

### Postman

```bash
brew install --cask postman
```

### Keka

```bash
brew install --cask keka
```
