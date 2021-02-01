---
title: "[Javascript] 실행 컨텍스트 개념"
date: 2021-02-01 16:13
categories: [Javascript]
---

# [Inside Javascript] Ch5.1

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

<br>

# Ch 5 실행 컨텍스트와 클로저

1. 실행 컨텍스트(Execution context)의 개념
2. 활성 객체(Activation objec)와 변수 객체(Variable Object)
3. 스코프 체인(Scoope chain)
4. 클로저(closure)

---

### 실행 컨텍스트

: 실행 가능한 코드를 형상화하고 구분하는 추상적인 개념, 실행 가능한 자바스크립트 코드 블록이 실행되는 환경

실행 가능한 코드 블록: 대부분의 경우 함수

### 실행 컨텍스트가 형성되는 경우

1. 전역 코드
2. eval() 함수로 실행되는 코드
3. 함수 안의 코드를 실행할 경우

코드 실행 → 실행 컨텍스트가 생성 → 실행 컨텍스트는 스택 안에 하나씩 차곡차곡 쌓임

- 제일 위(top)에 위치하는 실행 컨텍스트가 현재 실행되고 있는 컨텍스트

**실행 컨텍스트의 생성**

"현재 실행되는 컨텍스트에서 이 컨텍스트와 관련 없는 실행 코드가 실행되면, 새로운 컨텍스트가 생성되어 스택에 들어가고 제어권이 그 컨텍스트로 이동한다."

<br>

<5-1>

```jsx
console.log("This is global context");

function ExContext1() {
  console.log("This is ExContext1");
};

function ExContext2() {
  ExContext1();
  console.log("This is ExContext2");
};

ExContext2();
```

>This is global context <br>
This is ExContext1 <br>
This is ExContext2

<br>

새로운 함수 호출이 발생 → 새로운 컨텍스트가 만들어지고 실행 → 종료되면 반환 → 이 과정 반복 → 전역 실행 컨텍스트의 실행 완료 → 모든 실행 끝