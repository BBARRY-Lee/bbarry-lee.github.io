---
layout:   post
title:    "Let's create a GitHub Page 1"
subtitle: "GitHub Page로 개인 기술 블로그 만들기"
category: Development
tags:     Github-page
image:
  path:   /assets/img/2023-01-03/1.png
---
# Let's create a GitHub Page 1
<br>
<br>
<br>
<div align="center">
안녕하세요, Daisy 입니다 ☺️ <br>
<br>
제가 이번에 GitHub page를 통해 개인 블로그를 만들어보면서, <br>
그 과정을 쉽게 이해할 수 있도록 정리하여 공유해보려고 합니다. <br>
<br>
GitHub Page로 개인 블로그를 만드는 것에 관심이 있으시면, 해당 시리즈를 참고해주세요 :)<br>
</div>
<br>
<br>
<br>

---

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

## 1. GitHub 계정 생성

다음 [GitHub Web site](https://github.com/)에 접속해 `계정`을 생성해주세요. <br>
<br>


---

## 2. GitHub Setting
### 2-1. Repository 생성
이제 GitHub Page를 생성할 수 있는 초기 환경을 설정해봅니다.<br>
<br>
GitHub에 생성하신 계정으로 로그인 후, Repository를 새로 생성합니다.<br>
아래 예시화면과 같이 상단의 `Repositories → New`를 선택해주세요! <br><br>
![](/assets/img/2023-01-03/2.png)
<br>
<br>

---

### 2-2. Repository name 설정
다음으로 `Repository name`을 설정합니다. <br><br>
이 때, 중요한 부분은 `username`과 Repository name의 `스펠링`이 동일해야 합니다.<br>
필자의 username은 `BBARRY-Lee`로 대문자가 포함 돼 있는데, Repository name은 `소문자`로 생성했습니다.<br><br>
즉, username의 대소문자 상관없이 스펠링과 특수문자를 동일하게 작성해주신 후, 뒤에 `.github.io`를 붙여 써주세요.<br>
→ Repository name : `username.github.io`
>Ex : username : BBARRY-Lee → Repository name : `bbarry-lee.github.io`

![](/assets/img/2023-01-03/3.png) <br>

---

## 3. Local Setting
이제 Local 환경으로 돌아가 초기 환경설정을 진행해봅니다.<br>

필자는 Jekyll을 활용해 커스텀 후 배포과정에서 404 에러로 어려움이 있었지만<br>
이 과정에서 배운 것은 추후 Jekyll을 활용해 GitHub page를 배포 후 정상적으로 로딩되려면,<br>
Brunch 명이 `master`가 되어야 한다는 것이었습니다. <br><br>
![](/assets/img/2023-01-03/4.png)<br>
<br>
그래서 제가 소개드릴 방법은 Local에서 먼저 Brunch 명을 `master`로 초기 설정하고 시작하는 방법입니다. <br>
<br>

---

### 3-1. Local Directory 생성
우선 Github page를 통해 개인 블로그를 구현하기 위해서는 코드들이 필요하겠죠? ☺️<br>
<br>
Local 환경에 이 코드들을 저장할 위치를 선정합니다. <br>
필자는 적당한 위치에 Repository name과 동일한 Directory를 생성했습니다.<br>

자, 이제 터미널을 활용하여 `cd /Users/.../bbarry-lee.github.io` 명령어로 해당 Directory 위치로 이동합니다. <br>
그리고 `echo "Hello World" > Index.html` 명령어를 통해 "Hello world"가 기재된 `Index.html` 파일을 생성해봅니다. <br>


```shell
$ cd /Users/.../bbarry-lee.github.io
$ echo "Hello World" > Index.html
```
그러면, 해당 Directory에 `Index.html`이 정상적으로 생성될 거예요. <br>
<br>

---

### 3-2. Local Directory와 Repository 연결
다음으로 앞서 GitHub에서 생성한 Repository와 Local Directory을 연결해봅니다.<br>
<br>
다시 GitHub로 돌아와서 해당 Repository를 클릭하면 아래와 같은 페이지에 연결됩니다. <br>
(이후의 진행과정에서 본인의 Repository 클릭하여 해당 페이지 상단의 주소를 참고해주세요.)<br>
<br>
![](/assets/img/2023-01-03/5.png)<br>
<br>

---

### 3-3. Local Directory에 Git 초기설정
Chapter 3 초반에 추후 원활한 배포를 위해 Brunch 명을 `master`로 초기 설정을 진행한다고 했었습니다.<br><br>
먼저, `git init`이라는 명령어를 터미널에 입력해 해당 Directory를 `Git 저장소`로 설정해줍니다.<br>
그러면 해당 Local Directory에 `.git/`이라는 폴더가 생성되며, `master`라는 Brunch가 생성된 것을 확인할 수 있습니다.<br>
<br>
그리고 `git remote add origin https://github.com/BBARRY-Lee/bbarry-lee.github.io-.git`명령어를 입력하면, <br>
해당 Repository와 Directory가 연결됩니다.<br>

```shell
$ git remote add origin <Chapter 3-2에서 확인한 본인의 Repository 주소>
```

<br>
연결 여부는 터미널에 `git remote -v` 명령어를 입력하면 아래와 같이 확인 가능합니다.<br>
<br>
![](/assets/img/2023-01-03/6.png)<br>
<br>

---

## 4. GitHub Repository 반영
Chapter 3에서 `echo "Hello World" > Index.html` 명령어를 통해, `Index.html` 파일을 생성하였습니다.<br>
<br>
이제 이 파일을 GitHub에 업로드해봅니다.<br>
원활히 배포되려면 Local에서 작업한 코드를 해당 GitHub Repository에 꼭 업로드해주어야 합니다.<br>

다음 명령어들을 순차적으로 진행해주면 작업한 파일이 `add → commit → push` 순으로 진행 되고,<br>
최종적으로 push까지 진행주면 GitHub Repository에 업로드 됩니다.<br>

``` shell
$ git add .
$ git commit -m "first commit"
$ git push origin master
```

**add → commit → push까지 간단한 설명**
>1. add를 통해 Staging area 이동 (commit 전 임시저장)
>2. message와 함께 commit
>3. 지금까지의 commit(이력/버전)을 Repository로 push → Repository 업로드



그리고 다시 해당 Repository에 접속하면,`Index.html` 파일이 업로드된 모습을 확인할 수 있습니다.<br>
<br>
이제 정상적으로 배포된 모습을 확인하기 위해 `https://username.github.io`으로 접속 후,<br>
(username = 본인 username 변경, Ex : https://bbarry-lee.github.io)<br>
"Hello World" 텍스트가 확인되면 초기설정은 완료입니다.<br>

---
## 5. 마무리

다음 포스팅으로는 `Jekyll`을 활용하여, 본격적으로 GitHub page를 커스텀했던 과정을 소개해보겠습니다.
<br>
<br>

---

<!--more-->

<br><br>

<div align="center">
소통은 제가 공부하고 공유하는 원동력이 됩니다.<br>
해당 글이 도움이 되셨다면 소중한 격려와 응원 부탁드립니다 ☺️
</div>  