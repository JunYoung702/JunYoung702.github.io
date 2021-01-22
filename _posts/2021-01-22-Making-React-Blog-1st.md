---
layout: post
title: "리액트로 블로그 만들기 1일차"
date: 2021-01-22 01:40:32 +0900
author: JunYoung
categories: CS 웹프로그래밍
tags: Web React TypeScript
---

Jekyll 블로그가 이쁘고 좋긴한데 이미 만들어놓은 테마들
커스텀해서 수정하기가 너무 빡세서 공부할겸 React로 레이아웃만 따서
새로 만들어 보려고 계획했다.

<a href = "https://github.com/JunYoung702/React_TS_Blog">코드는 여기</a>

첫날에 한 것: 레이아웃 틀 잡기

기본적으로 탑메뉴-메인페이지 있고, 사이드바 버튼 누르면
사이드바가 나오게 구성하기로 했다.

<a href = "http://jekyllthemes.org/themes/adam-blog/">이렇게</a>

코드구조:

- App.tsx: isSidebarOn 변수에 따라 sidebar를 렌더링하거나 안하거나 결정
- page/Home.tsx: 메인 페이지
- component/Topmenu.tsx: 탑메뉴
- component/Sidebar.tsx: 사이드바

page 디렉토리에는 메인 페이지, 포스트 페이지, About 페이지, 태그 페이지, 카테고리 페이지
등이 들어갈 예정이다.

디자인을 참고하고 있는 Jekyll theme은 다음과 같다.

<a href = "http://jekyllthemes.org/themes/adam-blog/">1</a>

<a href = "http://jekyllthemes.org/themes/hydejack/">2</a>

<a href = "http://jekyllthemes.org/themes/jekyll-theme-chirpy/">3</a>

(지금 현재 테마로 쓰이고 있는 건 3번)

그외에 티스토리 테마도 괜찮아 보였다(다 똑같은 구조긴 하네 ㅋㅋㅋ)

현재 주요 과제로 생각되는 건

- 글 검색 구현하기
- 태그 구현하기
- 댓글 구현하기(아마 disqus를 쓰게 될듯)
- 애니매이션 구현하기(사이드바 나올때 페이지 옆으로 밀리는거나 참고 2번처럼,
  애플 홈페이지에서 제품설명나올때 자주나오는 애니매이션도 비슷한 느낌인듯)
- LaTex 수식, 코드 하이라이팅 구현

구현하는 데 <a href = "https://reactjsexample.com/">참고할 만한 사이트</a>를 찾았다.

주요 과제는 아니지만 하고싶은건

- 관리자 로그인 시스템
- 네이버나 티스토리 블로그같은 관리자 페이지 만들고 로그인해서 글쓰기, 수정 삭제 기능 구현하기

위 두가지는 서버사이드에서 돌아가야 할 것 같아서 라즈베리 파이로 홈서버 돌려서 올리고
그걸 깃헙에 다시 커밋할 생각이다. 아니면 AWS같은 클라우드 컴퓨팅 플랫폼을 쓰거나(Github Pages는 서버사이드에서 코드 실행이 안되니까)
