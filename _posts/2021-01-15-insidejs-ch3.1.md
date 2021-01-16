---
title: "[Inside Javascript] Ch3.1"
date: 2021-01-15 22:55
categories: [Javascript]
---

# [Inside Javascript] Ch3.1

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

자바스크립트의 값들은 크게 기본 타입과 참조 타입으로 나뉜다. 

기본 타입: 숫자(Number), 문자열(String), 불린값(Boolean), undefined, null

참조 타입: 객체(Object) - 배열(Array), 함수(Function), 정규표현식

---

# 3.1 자바스크립트 기본 타입

: 숫자, 문자열, 불린값, null, undefined

자바스크립트는 느슨한 타입 체크 언어이다. 변수를 선언할 떄 타입을 미리 정하지 않고, var라는 한 가지 키워드로만 변수를 선언한다. 이렇게 선언된 변수에는 어떤 타입의 데이터라도 저장하는 것이 가능하다. 따라서 자바스크립트는 변수에 어떤 형태의 데이터를 저장하느냐에 따라 해당 변수의 타입이 결정된다.

<예제 3-1>

```jsx
// 숫자 타입
var intNum = 10;
var floatNum = 0.1;

// 문자열 타입
var singleQuoteStr = 'single quote string';
var doubleQuoteStr  = "double quote string";
var singleChar = 'a';

// 불린 타입
var boolVar = true;

// undefined 타입
var emptyVar;

// null 타입
var nullVar = null;

console.log(
  typeof intNum,  // number
  typeof floatNum,   // number
  typeof singleQuoteStr,  // string
  typeof doubleQuoteStr,  // string
  typeof singleChar,  // string
  typeof boolVar,   // boolean
  typeof nullVar,   // object
  typeof emptyVar   // undefined
);
```


## 3.1.1 숫자

자바스크립트는 하나의 숫자형만 존재한다. 자바스크립트에서는 모든 숫자를 64비트 부동 소수점 형태로 저장하기 때문이다.

자바스크립트에서는 정수형이 따로 없고, 모든 숫자를 실수로 처리하므로 나눗셈 연산을 할 때는 주의해야 한다.

<예제 3-2>

```jsx
var num = 5 / 2;  // 모든 숫자를 실수 처리

console.log(num); // 출력값: 2.5
console.log(Math.floor(num)); // 출력값: 2
```

** 소수 부분을 버린 정수 부분만을 구하고 싶다면, 앞 예제와 같이 Math.floor() 자바스크립트 메서드를 사용하면 된다.


## 3.1.2 문자열

문자열은 작은 따옴표(')나 큰 따옴표(")로 생성한다. 자바스크립트에서는 C언어의 char 타입과 같이 문자 하나만을 별도로 나타내는 데이터 타입은 존재하지 않는다. 따라서 한 개의 문자를 나타내려면 길이가 1인 문자열을 사용해야 한다.

** 한 번 정의된 문자열은 변하지 않는다.

<예제 3-3>

```jsx
// str 문자열 생성
var str = 'test';
console.log(str[0], str[1], str[2], str[3]);  // 출력값: test

// 문자열의 첫 글자를 대문자로 변경?
str[0] = 'T';
console.log(str); // 출력값: test
```


## 3.1.3 불린값

자바스크립트는 true와 false 값을 나타내는 불린 타입을 가진다. 

## 3.1.4 null과 undefined

이 두 타입은 모두 자바스크립트에서 '값이 비어있음'을 나타낸다. 자바스크립트 환경 내에서 기본적로 값이 할당되지 않은 변수는 undefined 타입이며, undefined 타입 변수는 변수 자체의 값 또한 undefined이다. 이처럼 자바스크립트에서 undefined는 타입이자, 값을 나타낸다. 

자바스크립트에서는 null 타입 변수의 typeof 결과가 null이 아니라 object이다. 때문에 null 타입 변수인지를 확이할 때 typeof 연산자를 사용하면 안 되고, 일치 연산자(===)를 사용해서 변수의 값을 직접 확인해야 한다.

<예제 3-4>

```jsx
// null 타입 변수 생성
var nullVar = null;

console.log(typeof nullVar === null); // 출력값: false
console.log(nullVar === null);   // 출력값: true
```