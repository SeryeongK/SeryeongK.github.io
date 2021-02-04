---
title: "[ReactJS] NomadCoder-movie_app - Setup"
date: 2021-02-04 20:41
categories: [ReactJS]
---

# #1 Setup

## create-react-app

`npx create-react-app __direName`: 폴더 생성

![20210204-3.png](/assets/images/posts/2021-02-04/20210204-3.png)

** terminal - `code __dirName`: VSC에서 폴더 열기

<br>

---

- package.json에서 scripts의 start와 build 제외 삭제

## `npm start` ⇒ react application

![20210204-4.png](/assets/images/posts/2021-02-04/20210204-4.png)

`git remote add origin URL` : To add a new remote

(reference: [https://articles.assembla.com/en/articles/1136998-how-to-add-a-new-remote-to-your-git-repo#:~:text=To add a new remote%2C use the git remote add,tab of your Git repo](https://articles.assembla.com/en/articles/1136998-how-to-add-a-new-remote-to-your-git-repo#:~:text=To%20add%20a%20new%20remote%2C%20use%20the%20git%20remote%20add,tab%20of%20your%20Git%20repo))

<br>

---

## React의 동작 방식

React creates all the elements that you wirte on it. It creates them with Javascritp and pushes them with html. 모든 react application을 public>index.html>div 사이에 넣음

![20210204-5.png](/assets/images/posts/2021-02-04/20210204-5.png)

![20210204-6.png](/assets/images/posts/2021-02-04/20210204-6.png)

브라우저 상에서는 id가 root인 div 안에 Hello!!!의 내용을 담은 div를 찾을 수 있지만 아래의 실제 소스코드를 보면 id가 root인 div 안에 어떠한 코드도 없음을 알 수 있다.

<br>

![20210204-7.png](/assets/images/posts/2021-02-04/20210204-7.png)

```jsx
// index.js

import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

React는 소스코드에 처음부터 HTML을 넣지 않고, HTML에서 HTML을 추가하거나 제거하는 법을 알고 있다

⇒ application이 로드할 때

빈 HTML 로드, 그 다음 react가 component에 적은 것을 HTML에 밀어넣게 됨

<br>

---

리액트의 속도가 빠른 이유는 virtual, 즉 존재하지 않기 때문이다.