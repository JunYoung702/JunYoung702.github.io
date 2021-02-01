---
layout: post
title: "리액트로 블로그 만들기 3일차"
date: 2021-01-31 23:45:32 +0900
author: JunYoung
categories: CS 웹프로그래밍
tags: Web React JavaScript
---

markdown 파일을 불러와서 Post형태로 만들고 파일의 앞부분 일부를 잘라와서
미리보기 형태로 홈 화면에 띄우게 구현했다.

근데 디자인감각이 딸려서 예쁘게 만드는데는 좀 오래 걸릴듯...

구현하는 과정에서 파일이름을 props로 받아서 로딩하는데서 타입스크립트가 좀 말썽이라
일단 자바스크립트로 만들었다.

```jsx
class Post extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      postsrc: `../page/${props.postTitle}.md`,
      content: "",
    };
  }
  async componentDidMount() {
    const file = await import(`../page/${this.props.postTitle}`);
    const response = await fetch(file.default);
    const text = await response.text();
    const headerIdentifier = "---";
    const headerLast =
      text.lastIndexOf(headerIdentifier) + headerIdentifier.length;

    this.setState({
      content: text.substring(headerLast),
    });
  }
  render() {
    if (this.props.isHead)
      return (
        <div className="postHead">
          <div>{this.props.postTitle}</div>
          <Markdown children={this.state.content.slice(0, 300)} />
        </div>
      );
    else
      return (
        <div className="post">
          <Markdown children={this.state.content} />
        </div>
      );
  }
}
```

```jsx
import Titles from "../page/list.json";

function Postlist(props) {
  const PList = Titles.title.reverse().slice(0, props.num);
  console.log(PList);
  return PList.map((x) => <Post postTitle={x} isHead={true} key={x} />);
}
```

아마 서버사이드에서 폴더안에있는 파일 리스트를 출력하는 프로그램을 만들어서 그걸로 받아오게
처리하면 될 거 같긴 하다. 나중에 해봐야지...

mathjax랑 코드하이라이팅 적용하려면 마크다운 파서도 좀 개조해야할것 같다.
