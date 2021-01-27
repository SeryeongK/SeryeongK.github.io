---
title: "함수 객체: 함수도 객체다"
date: 2021-01-27 22:27
categories: [Javascript]
---

# [Inside Javascript] Ch4.2

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

<br>

# 4.2.1 자바스크립트에서는 함수도 객체다

: 함수의 기본 기능인 코드 샐행뿐만 아니라, 함수 자체가 일반 객체처럼 프로퍼티들을 가질 수 있다는 것이다.

<4-8>

```jsx
// add() 함수도 객체처럼 프로퍼티를 가질 수 있다.
// 함수 선언 방식로 add()함수 정의
function add(x, y) {
  return x + y;
}

// add() 함수 객체에 result, status 프로퍼티 추가
add.result = add(3, 2);
add.status = 'OK';

console.log(add.result);
console.log(add.status);
```

>5 <br>
OK

자바스크립트에서 함수는 특정 기능의 코드를 수행하는 역할뿐만 아니라, 일반 객체처럼 자신의 프로퍼티를 가질 수 있는 특별한 객체라고 볼 수 있다.


<br>

---

# 4.2.2 자바스크립트에서 함수는 값으로 취급된다

자바스크립트에서 함수는 객체다. 이는 함수도 일반 객체처럼 취급될 수 있다는 것을 말한다. 

### 자바스크립트 함수가 가능한 동작

- 리터럴에 의해 생성
- 변수나 배열의 요소, 객체의 프로퍼티 등에 할당 가능
- 함수의 인자로 전달 가능
- 함수의 리턴값으로 리턴 가능
- 동적으로 프로퍼티를 생성 및 할당 가능

⇒ 함수를 일급(First Class) 객체라고 부른다

** 일급 객체: 위의 기능이 모두 가능한 객체

### 함수

- 입력한 값을 받아 처리한 다음 그 결과를 반환하는 구조
- 일급 객체, 함수가 일반 객체처럼 값(value)으로 취급된다
- 변수나 객체, 배열 등에 값으로도 저장할 수 있다
- 다른 함수의 인자로 전달한다거나 함수의 리턴값으로도 사용 가능하다

<br>

## 4.2.2.1 변수나 프로퍼티의 값으로 할당

<4-9>

```jsx
// 변수나 프로퍼티에 함수값을 할당하는코드
//변수에 함수 할당
var foo = 100;
var bar = function () { return 100; };
console.log(bar());

// 프로퍼티에 함수 할당
var obj = {};
obj.baz = function () { return 200; }
console.log(obj.baz());
```

>100 <br>
200

<br>

## 4.2.2.2 함수 인자로 전달

<4-10>

```jsx
// 함수를 다른 함수의 인자로 넘킨 코드
// 함수 표현식으로 foo() 함수 생성
var foo = function(func) {
  func(); // 인자로 받은 func() 함수 호출
}

// foo() 함수 실행
foo(function() {
  console.log('Function can be used as the argument.');
});
```

>Function can be used as the argument.

<br>

## 4.2.2.3 리턴값으로 활용

<4-11>

```jsx
// 함수를 다른 함수의 리턴값으로 활용한 코드
// 함수를 리턴하는 foo() 함수 정의
var foo = function() {
  return function() {
    console.log('this function is the return value.')
  };
};

var bar = foo();
bar();
```

>this function is the return value

<br>

---

## 4.2.3 함수 객체의 기본 프로퍼티

함수는 객체다. 함수 역시 일반적인 객체의 기능에 추가로 호출했을 때 정의된 코드를 실행하는 기능을 가지고 있다. 또한, 일반 객체와는 다르게 추가로 함수 객체만의 표준 프로퍼티가 정의되어 있다.

<4-12>

```jsx
// add() 함수 객체 프로퍼티를 출력하는 코드
function add(x, y) {
  return x + y;
}

console.dir(add);
```

![20210127-1.png](/assets/images/posts/2021-01-27/20210127-1.png)

ECMA5 '모든 함수가 length와 prototype 프로퍼티를 가져야 한다'

`name` 프로퍼티: 함수의 이름을 나타낸다. 만약 이름이 없는 익명 함수라면 name 프로퍼티는 빈 문자열이 된다.

`caller` 프로퍼티: 자신을 호출한 함수

`arguments` 프로퍼티: 함수를 호출할 때 전달된 인자값을 나타낸다.  

cf) arguments 객체: 함수를 호출할 때 호출된 함수의 내부로 인자값과 함께 전달되며, arguments 프로퍼티와 유사하게 함수를 호출할 때 전달 인자값의 정보를 제공해준다.

`__proto__` 프로퍼티: 모든 자바스크립트 객체는 자신의 프로토타입을 가리키는 [[Prototype]]라는 내부 프로퍼티를 가지는데 크롬 브라우저에서는 [[Prototype]]이라는 내부 프로퍼티가 바로 **proto** 프로퍼티로 구현되어 있다.

<br>

Function.prototype 객체(Empty() 함수): 함수 객체의 부모 역할을 하는 프로토타입 객체

- constructor 프로퍼티
- toString() 메서드
- apply(thisArg, argArray) 메서드
- call(thisArg, [, arg1 [,arg2, ]]) 메서드
- bind(thisArg, [, arg1 [,agr2, ]]) 메서드

<br>

---

## 4.2.3.1 length 프로퍼티

- 모든 함수가 가져야 하는 표준 프러퍼티
- 함수가 정상적으로 실행될 때 기대되는 인자의 개수 = 함수를 작성할 때 정의한 인자 개수

<4-13>

```jsx
// 함수 객체의 length 프로퍼티
function func0() {

}

function func1(x) {
  return x;
}

function func2(x, y) {
  return x + y;
}

function func3(x, y, z) {
  return x + y + z;
}

console.log('function0.length - ' + func0.length);
console.log('function0.length - ' + func1.length);
console.log('function0.length - ' + func2.length);
console.log('function0.length - ' + func3.length);
```

>function0.length - 0 <br>
function0.length - 1 <br>
function0.length - 2 <br>
function0.length - 3

<br>

---

## 4.2.3.2 prototype 프로퍼티

### prototype 프로퍼티 vs [[Prototype]] 프로퍼티

공통점: 프로토타입 객체를 가리킨다

prototype 프로퍼티

- 함수 객체가 가짐
- 함수가 생성될 때 만들어짐
- constructor 프로퍼티 하나만 있는 객체를 가리킴
- 함수가 생성자로 사용될 때 이 함수를 통해 생성된 객체의 부모 역할을 하는 프로토타입 객체를 가리킴

[[Prototype]]

- 모든 객체에 있는 내부 프로퍼티
- 객체 입장에서 자신의 부모 역할을 하는 프로토타입 객체를 가리킴

자바스크립트에서는 함수를 행성할 때, 함수 자신과 연결된 프로토타입 객체를 동시에 생성하며, 이 둘은 각각 prototype과 constructor라는 프로퍼티로 서로를 참조하게 된다.

![20210127-2.png](/assets/images/posts/2021-01-27/20210127-2.png)

⇒ 함수 객체와 프로토타입 객체는 서로 밀접하게 연결돼 있다.

<4-14>

```jsx
// MyFunction() 함수 정의
function myFunction() {
  return true;
}

console.dir(myFunction.prototype);
console.dir(myFunction.prototype.contructor);
```
![20210127-3.png](/assets/images/posts/2021-01-27/20210127-3.png)
