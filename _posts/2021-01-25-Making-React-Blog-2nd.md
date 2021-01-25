---
layout: post
title: "리액트로 블로그 만들기 2일차"
date: 2021-01-25 22:30:32 +0900
author: JunYoung
categories: CS 웹프로그래밍
tags: Web React TypeScript
---

사이드바 애니메이션을 구현했다.

<a href = "https://www.w3schools.com/howto/howto_js_sidenav.asp">Reference</a>

sidebar 버튼을 클릭하면 다음 함수를 실행한다.

```typescript
sidebarToggle = () => {
  const sb = document.getElementById("sidebarLayout")!;
  const m = document.getElementById("mainpage")!;
  const t = document.getElementById("toppage")!;
  if (this.state.isSidebarOn) {
    sb.style.width = "0px";
    m.style.marginLeft = "0px";
    t.style.marginLeft = "0px";
  } else {
    sb.style.width = "250px";
    m.style.marginLeft = "250px";
    t.style.marginLeft = "250px";
  }

  this.setState({ isSidebarOn: !this.state.isSidebarOn });
};
```

```css
.sidebar {
  display: flex;
  position: absolute;
  width: 0px;
  bottom: 0px;
  top: 0px;
  z-index: 1;
  overflow-x: hidden;
  transition: 0.5s;
}
```

애니메이션 만드는게 어려울 줄 알았는데 생각보다 쉽게 해결됐다.
