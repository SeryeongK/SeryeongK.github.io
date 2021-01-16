---
title: "[Inside Javascript] Ch3.2"
date: 2021-01-15 22:00
categories: [Javascript]
---

# [Inside Javascript] Ch3.2

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

자바스크립트에서 숫자, 문자열, 불린값, null, undefined 같은 기본 타입을 데외한 모든 값은 객체다. 따라서 배열, 함수, 정규표현식 등도 모두 결국 자바스크립트 객체로 표현된다. 

자바스크립트에서 객체는 단순히 `이름(key):값(value)` 형태의 프로퍼티들을 저장하는 컨테이너로서 컴퓨터 과학 분야에서 해시(Hash)라는 자료구조와 상당히 유사한다. 

- 기본 타입: 하나의 값만을 가짐
- 객체(참조 타입): 여러 개의 프로퍼티(메서드, 기본 타입의 값을 포함하거나, 다른 객체를 가리킬 수도 있음)들을 포함 가능

***
# 3.2.1 객체 생성

자바스크립트에서는 클래스라는 개념이 없고, 객체 리터럴이나 생성자 함수 등 별도의 생성 방식이 존재한다.

>### 자바스크립트에서 객체를 생성하는 방법

1. 기본 제공 Object() 객체 생성자 함수를 이용
2. 객체 리터럴을 이용
3. 생성자 함수를 이용

## 3.2.1.1 Object() 생성자 함수 이용

<예제 3-5>

```jsx
// Object() 생성자 함수를 통한 객체 생성

// Object()를 이용해서 foo 빈 객체 생성
var foo = new Object();

// foo 객체 프로퍼티 생성
foo.name = 'foo';
foo.age = 30;
foo.gender = 'male';

console.log(typeof foo);  // 출력값: Object
console.log(foo);  // 출력값: { name: 'foo', age: 30, gender: 'male' }
```

object
{ name: 'foo', age: 30, gender: 'male' }

object

{ name: 'foo', age: 30, gender: 'male' }

## 3.2.1.2 객체 리터럴 방식 이용

** 리터럴: 표기법

객체 리터럴 방식은 간단한 표기법만으로도 객체를 생성할 수 있는 자바스크립트의 강력한 문법이다.

- 중괄호({})를 이용해서 객체를 생성
- { } 안에 아무것도 적지 않은 경우: 빈 객체 생성
- `{ 프로퍼티 이름: 프로퍼티 값 }` : 해당 프로퍼티가 추가된 객체를 생성 가능
** 프로퍼티 이름: 문자열이나 숫자
** 프로퍼티 값: 자바스크립트의 값을 나타내는 어떤 표현식, 이 값이 함수일 경우 이러한 프로퍼티를 메서드라고 부른다.

<예제 3-6>

```jsx
// 객체 리터럴 방식으로 객체 생성

var foo = {
  name : 'foo',
  age : 30,
  gender: 'male'
};

console.log(typeof foo);
console.log(foo);
```

object
{ name: 'foo', age: 30, gender: 'male' }

object

{ name: 'foo', age: 30, gender: 'male' }

## 3.2.1.3 생성자 함수 이용

** 생성자 함수: 함수를 통해서 객체를 생성하는 함수

***
# 3.2.2 객체 프로퍼티 읽기/쓰기/갱신

객체는 새로운 값을 가진 프로퍼티를 생성하고, 생성된 프로퍼티에 접근해서 해당 값을 읽거나 또는 원하는 값으로 프로퍼티의 값을 갱신할 수 있다.

### 객체 프로퍼티에 접근하기 위한 방법

- 대괄호([]) 표기법
- 마침표(.) 표기법

<예제 3-7>

```jsx
// 객체 리터럴 방식을 통한 foo 객체 생성
var foo = {
  name : 'foo',
  major : 'computer science'
};

// 객체 프로퍼티 읽기
console.log(foo.name);
console.log(foo['name']);
console.log(foo.nickname);

// 객체 프로퍼티 갱식
foo.major = 'electronics engineering';
console.log(foo.major);
console.log(foo['major']);

// 객체 프로퍼티 동적 생성
foo.age = 30;
console.log(foo.age);

// 대괄호 표기법만을 사용해야 할 경우
foo['full-name'] = 'foo bar';
console.log(foo['full-name']);
console.log(foo.full-name);
console.log(foo.full);
console.log(name);
```

>foo<br>
foo<br>
undefined<br>
electronics engineering<br>
electronics engineering<br>
30<br>
foo bar<br>
NaN<br>
undefined<br>
undefined<br>

1. 프로퍼티 읽기

객체의 프로퍼티 접근은 대괄호 표기법이나 마침표 표기법으로 가능하다. 마침표 표기법은 객체 다음에 마침표를 찍고 원하는 속성값을 적으면 된다. 대괄호 표기법은 접근하려는 객체의 프로퍼티를 문자열 형태로 만든 다음 대괄호를 둘러싸면 된다. 여기서 주의할 점은 대괄호 표기법에서는 접근하려는 프로퍼티 이름을 문자열 형태로 만들어야 한다는 것이다. 

자바스크립트에서는 대괄호 표기법에서 접근하려는 프로퍼티 이름을 문자열 형태로 만들지 않으면 모든 자바스크립트 객체에서 호출 가능한 `toSting()`이라는 메서드를 자동으로 호출해서 이를 문자열로 바꾸려는 시도를 한다. 만약 객체에 없는 프로퍼티에 접근하는 경우는 undefined 값이 출력된다. 

2. 프로퍼티 갱신

프로퍼티에 접근해서 객체의 기존 프로퍼티값을 갱신할 수도 있다. 

예) `foo['major'] = 'electronics engineering'`

3. 프로퍼티 동적 생성

객체가 생성된 후에도 동적으로 프로퍼티를 생성해서, 해당 객체에 추가할 수 있다.

자바스크립트 객체의 프로퍼티에 값을 할당할 때, 프로퍼티가 이미 있을 경우는 해당 프로퍼티의 값이 갱신되지만, 객체의 해당 프로퍼티가 없을 경우에는 새로운 프로퍼티가 동적으로 생성된 후 값이 할당된다. 

4. 대괄호 표기법만을 사용해야하는 경우

: 접근하려는 프로퍼티가 표현식이거나 예약어일 경우

<NaN (Not a Number) 값>

수치 연산을 해서 정상적인 값을 얻지 못할 때 출력되는 값

***
# 3.2.3 for in 문과 객체 프로퍼티 출력

for in 문을 사용하면, 객체에 포함된 모든 프로퍼티에 대해 루프를 수행할 수 있다. 

<예제 3-8>

```jsx
// 객체 리터럴을 통한 foo 객체 생성
var foo = {
  name: 'foo',
  age: 30,
  major: 'computer science'
};

// for in 문을 이용한 객체 프로퍼티 출력
var prop;
for (prop in foo) {
  console.log(prop, foo[prop]);
};
```

>name foo<br>
age 30<br>
major computer science

***
## 3.2.4 객체 프로퍼티 삭제

객체의 프로퍼티를 `delete` 연산자를 이용해 즉시 삭제할 수 있다. 여기서 주의할 점은 `delete` 연산자는 객체의 프로퍼티를 삭제할 뿐, 객체 자체를 삭제하지는 못한다는 것이다.

<p. 45>

```jsx
// 객체 리터럴을 통한 foo 객체 생성
var foo = {
  name: 'foo',
  nickname: 'babo'
};

console.log(foo.nickname);
delete foo.nickname;
console.log(foo.nickname);

delete foo;
console.log(foo.name);
```
> babo<br> undefined<br>foo