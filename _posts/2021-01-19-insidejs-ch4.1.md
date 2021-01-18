---
title: "함수 정의"
date: 2021-01-19 06:57
categories: [Javascript]
---


# [Inside Javascript] Ch4.1

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

<br>

자바스크립트에서 함수를 생성하는 방법 3가지

- 함수 선언문(function statement)
- 함수 표현식(function expression)
- Function() 생성자 함수

<br>

***
# 4.1.1 함수 리터럴

구성요소

1. function 키워드: 자바스크립트 함수 리터럴은 function 키워드로 시작한다.
2. 함수명: 함수명은 함수 몸체의 내부 코드에서 자신을 재귀적으로 호출하거나 또는 자바스크립트 디버거가 해당 함수를 구분하는 식별자로 사용된다. <b>여기서 주목할 점은 함수명은 선택 사항이라는 것이다.</b> 자바스크립트에서는 함수명이 없는 함수를 익명 함수라 한다.
3. 매개변수 리스트
4. 함수 몸체: 실제 함수가 호출됐을 때 실행되는 코드 부분

<br>

***
# 4.1.2 함수 선언문 방식으로 함수 생성하기

<b>반드시 함수명이 정의되어 있어야 한다.</b>

<4-1>

```jsx
// add() 함수 생성(함수 선언문 방식)
// add() 함수 선언문
function add(x, y) {
  return x + y;
};

console.log(add(3, 4));
```

>7

<br>

***
# 4.1.3 함수 표현식 방식으로 함수 생성하기

함수 표현식
: 함수 리터럴로 하나의 함수를 만들고, 여기서 생성된 함수를 변수에 할당하여 함수를 생성하는 것

<4-2>

```jsx
// add() 함수 생성(함수 표현식 방식)
// add() 함수 표현식
var add = function (x, y) {
  return x + y;
}

var plus = add;

console.log(add(3, 4));
console.log(plus(5, 6));
```

>7<br>
11

>add 변수: 함수 리터럴로 생성한 <b>함수를 참조하는 변수</b>, 함수 이름이 아님

** 익명 함수(anonymous function): 이름이 없는 함수 형태

<4-3>

```jsx
// 기명 함수 표현식의 함수 호출 방법
var add = function sum(x, y) {
  return x + y;
};

console.log(add(3, 4));
console.log(sum(3, 4));
```

>7<br>
ReferenceError: sum is not defined

>에러가 발생하는 이유: <b>함수 표현식에서 사용된 함수 이름이 외부 코드에서 접근 불가능하기 때문</b>

<4-4>

```jsx
// 함수 표현식 방식으로 구현한 팩토리얼 함수
var factorialVar = function factorial(n) {
  if(n <= 1) {
    return 1;
  }
  return n * factorial(n-1);
};

console.log(factorialVar(3));
console.log(factorial(3));
```

>6<br>
ReferenceError: factorial is not defined

### function statement와 function expression에서의 세미콜론

일반적으로 자바스크립트 코드를 작성할 때 함수 선언문 방식으로 선언된 함수의 경우는 함수 끝에 세미콜론(;)을 붙이지 않지만, 함수 표현식 방식의 경우는 세미콜론(;)을 붙이는 것을 권장한다. 

<br>

***
# 4.1.4 Function() 생성자 함수를 통한 함수 생성하기

자바스크립트의 함수도 Function()이라는 기본 내장 생성자 함수로부터 생성된 객체라고 볼 수 있다. 함수 선언문이나 함수 표현식 방식도 내부적으로는 Function() 생성자 함수로 함수가 생성된다고 볼 수 있다.

### Function() 생성자 함수

```jsx
new Function (arg1, arg2, ..., argN, functionBody)
```

arg1, arg2, ..., argN: 함수의 매개변수

functionBody: 함수가 호출될 때 실행될 코드를 포함한 문자열

<4-5>

```jsx
// Function() 생성자 함수를 이용한 add() 함수 생성
var add = new Function('x', 'y', 'return x + y');
console.log(add(3, 4));
```

>7

<br>

***
# 4.1.5 함수 호이스팅

: 함수 선언문 형태로 정의한 함수의 유효 범위는 코드의 맨 처음부터 시작한다.

더글라스 크락포드 "함수 호이스팅은 함수를 사용하기 전에 반드시 선언해야 한다는 규칙을 무시하므로 코드의 구조를 엉성하게 만들 수도 있다. 함수 표현식 사용을 권장"

<4-6>

```jsx
// 함수 선언문 방식과 함수 호이스팅

add(2, 3);

// 함수 선언문 형태로 add() 함수 정의 
function add(x, y) {
  return x + y;
}

add(3,4);
```

>5<br>
7

<4-7>

```jsx
// 함수 표현식 방식과 함수 호이스팅

add(2, 3);

// 함수 표현식 형태로 add() 함수 정의 
var add = function (x, y) {
  return x + y;
}

add(3,4);
```

>uncaught type error<br>
7

함수 호이스팅의 발생 원인: 자바스크립트의 변수 생성(Instantiation)과 초기화(Intialization)의 작업이 분리돼서 진행되기 때문