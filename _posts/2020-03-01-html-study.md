---
layout: post
title: "생활코딩 Web1 HTML/인터넷"
date:   2020-03-01 12:21:32 +0900
author: JunYoung
categories: 프로그래밍
tags:	Web Github 
---

<h1>HTML</h1>
<h2>기본개념</h2>
문서(웹페이지)의 구조를 논리적으로 서술하는 마크업 언어. 대충 텍과 같은 부류이다.

<h2>문법</h2>

* HTML은 태그를 사용해서 명령어의 범위를 지정하고 명령어를 사용한다.

    예시)

    ```html
    <a href = "https://junyoung702.github.io"> 블로그 링크 </a>
    ```

    <a href = "https://junyoung702.github.io"> 블로그 링크 </a>

* 속성: 태그에 추가적인 정보를 표시하기 위해서 만들어진 것

    예시)

    ```html
    <img src="https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7648.png">
    ```

    <img src="https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7648.png">

    위 예시에서는 src가 속성이다.

* 문서 시작할때

    ```html
    <!DOCTYPE html>
    ```

    을 붙여주면 브라우저가 html파일로 인식한다.

<h1>인터넷</h1>

<h2>기본개념</h2>
클라이언트가 요청을 보내면 서버가 html파일을 보내고 그걸 받은 클라이언트의 웹 브라우저가 파일을 해석해서 우리가 보는 웹페이지를 렌더링한다.

<a href="https://www.apache.org/">Apache</a>와 같은 서버 프로그램을 깔면 개인 컴퓨터도 서버로 사용할 수 있다. 로컬에 있는 파일들 보내주면됨.

웹사이트들이 하위 페이지들을 www.github.com/JunYoung702 와 같이 /로 구분하는 방식과 컴퓨터 디렉토리가 /home/junyoung 과 같이 하위 디렉토리를 /로 구분하는 방식이 같은 게 괜히 그런 게 아니었다... 그냥 서버에 같은 방식으로 페이지들이 저장되어 있는것인듯.