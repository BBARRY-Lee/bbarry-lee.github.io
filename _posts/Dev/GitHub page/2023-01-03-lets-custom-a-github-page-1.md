---
layout:   post
title:    "[Mac] Let's custom a GitHub Page 1"
subtitle: "[Mac] GitHub Page로 개인 기술 블로그 만들기"
category: Dev
tags:     GitHub-Page Git Mac
image:
  path:   /assets/img/2023-01-03/1.png
---
# [Mac] Let's custom a GitHub Page 1
<br><br><br>

안녕하세요, Daisy 입니다 ☺️ <br>
<br>
이번에는 Jekyll을 활용해 GitHub page를 custom 해보았으며, <br>
그 과정을 쉽게 이해할 수 있도록 정리하여 공유해보고자 합니다. <br>
<br>
> GitHub Page로 개인 블로그를 만드는 것에 관심이 있으시면, [해당 시리즈](/tag-github-page/)를 참고해주세요 :)<br>

<br><br><br>

---
<!--more-->
<!-- Table of contents -->
* this unordered seed list will be replaced by the toc
{:toc}

<!-- text -->
## 1. About Jekyll (지킬)
### 1-1. Jekyll의 간략한 소개
`Jekyll`은 정적인 웹사이트 생성기로 `Ruby`를 기반으로 제작 되었으며 `Markdown` 방식의 글쓰기가 가능합니다. <br>
또한, `Markdown`, `_config.yml`등 파일들을 기반으로 `_site` 폴더에 output을 생성하고 이를 GitHub에서 커밋 후,<br>
해당 url로 접속하면 웹으로 구현된 블로그를 확인할 수 있습니다.<br>
<br>
이러한 편리한 도구를 많은 사람들이 활용하여 테마를 제작해 공유 혹은 판매하고 있습니다.<br>
즉, 기본 형태가 갖추어져 있는 템플릿을 어느정도 custom만 하면, 포스팅에 집중할 수 있습니다.<br>
<br>
여러 후보 사이트들이 있으며 예시로 아래 3가지가 있습니다.<br>
> 1. [jekyllthemes.io](https://jekyllthemes.io/)<br>
> 2. [jekyllthemes.dev](https://jekyllthemes.dev/)<br>
> 3. [jekyll-themes.com](https://jekyll-themes.com/free/)<br>

이외에도 더 많은 사이트와 테마들이 있으니 구글링을 통해 스타일에 맞는 테마를 선택해주시면 됩니다.<br>
<br>

---

### 1-2. Jekyll Theme 선택
필자는 여러 탐색 끝에 `Hydejack Theme`를 선택했습니다.<br>
> [Hydejack Theme download page](https://hydejack.com/download/)<br>


그 이유는 깔끔한 애니메이션과 사이드에 위치한 Category가 독자와 필자 모두 본문에 집중하기 좋은 구조라고 생각합니다.<br>
특히 PRO 버전의 기능들이 마음에 들었고, 직접 기능을 추가해볼 수도 있지만 시간 단축을 위해 정식으로 구매했습니다.<br>
<br>
무료도 기본에 충실한 좋은 기능이니 사용해볼만 합니다.<br>
(시간이 되시면 무료로 시작해서 직접 기능을 추가해주시면 됩니다!)<br>
<br>
Free와 PRO 버전의 기능 차이는 아래와 같으며, 해당 페이지에서 Free와 PRO 버전 중 선택하면 됩니다. <br>
<br>
![](/assets/img/2023-01-03/8.png)<br>
<br>

---

### 1-3. Jekyll Theme 다운로드
맨 하단의 2개의 버튼 중 `Free` 부분의 Download를 선택하면 해당 GitHub로 연결되며<br>
첫번째 Source code(zip)을 선택하면 해당 zip을 다운로드 받을 수 있습니다.<br>
<br>
![](/assets/img/2023-01-03/9.png)<br>
<br>

---

`PRO` 버전은 결제를 끝내면, 입력한 이메일 주소로 메일이 오며 아래 View content를 선택하면 됩니다.<br>
<br>
![](/assets/img/2023-01-03/10.png)<br>
<br>
그리고 첫번째 부분을 Download 해주면 동일하게 zip 파일을 다운로드 됩니다.<br>
<br>
![](/assets/img/2023-01-03/11.png)<br>
<br>

---

이렇게 zip 파일까지 다운로드 했으면 다음 과정은 더 간단합니다.<br>
<br>

앞서 생성했던 `Index.html`을 삭제해주고 zip 폴더를 압축해제한 뒤, <br>
아래와 같이 압축 해제한 파일들을 모두 Local Directory로 옮겨주면 됩니다. (Free와 Pro 동일)<br>
<br>
![](/assets/img/2023-01-03/12.png)<br>

---

## 2. Setting
이제 다운로드받은 Jekyll Theme를 적용하기 위해 먼저 `Ruby`가 설치되어 있어야 합니다.<br>
<br>
먼저 터미널에 `ruby -v` 명령어로 Ruby의 버전 확인 및 설치 여부 확인 후,<br>
다음 명령어 `gem install jekyll bundler`로 Jekyll을 설치하면 됩니다.<br>

그리고 `bundle install`과 `bundle exec jekyll serve`를 순차적으로 터미널에 입력하면 아래와 같이 출력되며,<br>
``` shell
$ ruby -v
$ bundle install
$ bundle exec jekyll serve
```
<br>
![](/assets/img/2023-01-03/13.png)<br>

`http://127.0.0.1:4000`으로 접속하면, Hydejack Theme가 적용된 기본 화면을 확인할 수 있습니다.<br>
최종적으로 다음과 같이 확인되면 Jekyll Theme 초기설정은 완료입니다.<br>
<br>
![](/assets/img/2023-01-03/14.png)<br>

---

## 3. 마무리

다음 포스팅으로는 Hydejack Theme를 본격적으로 custom 해보겠습니다.
<br><br>

<!-- Next series [Let's custom a GitHub Page 1](lets-custom-a-github-page-1){:.heading.flip-title}
{:.read-more} -->

---


<br><br>

<!-- Closing -->
<div align="center">
소통은 제가 공부하고 공유하는 원동력이 됩니다.<br>
해당 글이 도움이 되셨다면 소중한 격려와 응원 부탁드립니다 ☺️
</div>  
