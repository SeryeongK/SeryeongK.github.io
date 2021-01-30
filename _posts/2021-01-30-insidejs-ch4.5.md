---
title: "프로토타입 체이닝"
date: 2021-01-30 16:26
categories: [Javascript]
---


# [Inside Javascript] Ch4.5

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

<br>

# 4.5.1 프로토타입의 두 가지 의미

함수 객체의 **prototype 프로퍼티**와 객체의 숨은 프로퍼티인 **[[Prototype]] 링크**를 구분해야 한다는 점이다.

**자바스크립트의 객체 생성 규칙**

자바스크립트에서 모든 객체는 자신을 생성한 생성자 함수의 prototype 프로퍼티가 가리키는 프로토타입 객체를 자신의 부모 객체로 설정하는 [[Prototype]] 링크로 연결한다.

<br>

<4-37>

```jsx
// prototype 프로퍼티와 [[Prototype]] 링크 구분
// Person 생성자 함수
function Person(name) {
  this.name = name;
}

// foo 객체 생성
var foo = new Person('foo');
console.dir(Person);
console.dir(foo);
```

![20210130-6.png](/assets/images/posts/2021-01-30/20210130-6.png)


** __proto__프로퍼티([[Prototype]] 프로퍼티): 모든 객체에 존재하는 숨겨진 프로퍼티로, 객체 자신의 프로토타입 객체를 가리키는 참조 링크 정보

---

# 4.5.2 객체 리터럴 방식으로 생성된 객체의 프로토타입 체이닝

- 자바스크립트에서 객체는 자신의 프로퍼티뿐만이 아니라, 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티 또한 마치 자신의 것처럼 접근하는 게 가능하다

<br>

<4-38>

```jsx
// 객체 리터럴 방식에서의 프로토타입 체이닝
var myObject = {
  name: 'foo',
  sayName: function() {
    console.log('My Name is ' + this.name);
  }
};

myObject.sayName();
console.log(myObject.hasOwnProperty('name'));
console.log(myObject.hasOwnProperty('nickname'));
myObject.sayNickName();
```

>My Name is foo <br>
true <br>
false <br>
Uncaught TypeError: Object #\<Object> has no method 'sayNickName'


`hasOwnProperty()` 메서드: 이 메서드를 호출한 객체에 인자로 넘긴 문자열 이름의 프로퍼티나 메서드가 있는지 체크하는 자바스크립트 표준 API 함수

<br>

### 프로토타입 체이닝

: 자바스크립트에서 특정 객체의 프로퍼티나 메서드에 접근하려고 할 때, 해당 객체에 접근하려는 프로퍼티 또는 메서드가 없다면 [[Prototype]] 링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티를 차례대로 검색하는 것

### `Object.prototype` 객체

: 자바스크립트 모든 객체의 조상 역할을 하는 객체, 자바스크립트 모든 객체가 호출할 수 있는 toString(), hasOwnProperty() 등과 같은 표준 메서드를 제공하고 있다.

<br>

---

# 4.5.3 생성자 함수로 생성된 객체의 프로토타입 체이닝

"자바스크립트에서 모든 **객체**는 자신을 생성한 **생성자 함수**의 **prototype 프로퍼티가 가리키는 객체**를 자신의 **프로토타입 객체(부모 객체)**로 취급한다."

<br>

<4-39>

```jsx
// 생성자 함수 방식에서의 프로토타입 체이닝
// Person() 생성자 함수
function Person(name, age, hobby){
  this.name = name;
  this.age = age;
  this.hobby = hobby;
}

// foo 객체 생성
var foo = new Person('foo', 30, 'tennis');

// 프로토타입 체이닝
console.log(foo.hasOwnProperty('name'));

// Person.prototype 객체 출력
console.dir(Person.prototype);
```

![20210130-7.png](/assets/images/posts/2021-01-30/20210130-7.png)


<br>

---

# 4.5.4 프로토타입 체이닝의 종점

: `Object.prototype` 객체

⇒ 객체 리터럴 방식이나 생성자 함수 방식에 상관없이 모든 자바스크립트 객체는 프로토타입 체이닝으로 Object.prototypr 객체가 가진 프로퍼티와 메서드에 접근하고, 서로 공유가 가능하다는 것을 알 수 있다.

- `hasOwnProperty()`나 `isPrototypeOf()` 등과 같이 모든 객체가 호출 가능한 표준 메서드들이 정의되어 있다.

<br>

---

# 4.5.5 기본 데이터 타입 확장

자바스크립트의 숫자, 문자열, 배열 등에서 사용되는 표준 메서드들의 경우, 이들의 프로토타입인 Number.prototype, String.prototype, Array.prototype 등에 정의되어 있다. 

<4-40>

```jsx
// String 기본 타입에 메서드 추가
String.prototype.testMethod = function() {
  console.log('This is the String.prototype.testMethod()');
};

var str = "this is test";
str.testMethod();

console.dir(String.prototype);
```

![20210130-8.png](/assets/images/posts/2021-01-30/20210130-8.png)


<br>

---

# 4.5.6 프로토타입도 자바스크립트 객체다

함수가 생성될 때, 자신의 prototype 프로퍼티에 연결되는 프로토타입 객체는 디폴트로 constructor 프로퍼티만을 가진 객체다. 당연히 프로토타입 객체 역시 자바스크립트 객체이므로 일반 객체처럼 동적으로 프로퍼티를 추가/삭제하는 것이 가능하다. 그리고 이렇게 변경된 프로퍼티는 실시간으로 프로토타입 체이닝에 반영된다.

<4-41>

```jsx
// 프로토타입 객체의 동적 메서드 생성 예제 코드

// Person() 생성자 함수
function Person(name) {
  this.name = name;
}

// foo 객체 생성
var foo = new Person('foo');

//foo,sayHello)();

// 프로토타입 객체에 sayHello() 메서드 정의
Person.prototype.sayHello = function() {
  console.log('Hello');
}

foo.sayHello();
```

>Hello

<br>

---

# 4.5.7 프로토타입 메서드와 this 바인딩

<4-42>

```jsx
// 프로토타입 메서드와 this 바인딩
// Person() 생성자 함수
function Person(name) {
  this.name = name;
}

// getName() 프로토타입 메서드
Person.prototype.getName = function() {
  return this.name
};

// foo 객체 생성
var foo = new Person('foo');

console.log(foo.getName());

//Person.prototype 객체에 name 프로퍼티 동적 추가
Person.prototype.name = 'person';

console.log(Person.prototype.getName());
```

>foo <br>
person

<br>

---

# 4.5.8 디폴트 프로토타입은 다른 객체로 변경이 가능하다

<4-43>

```jsx
// 프로토타입 객체 변경
// Person() 생성자 함수
function Person(name) {
  this.name = name;
}
console.log(Person.prototype.constructor);

// foo 객체 생성
var foo = new Person('foo');
console.log(foo.country);

// 디폴트 프로토타입 객체 변경
Person.prototype = {
  country: 'korea',
};
console.log(Person.prototype.constructor);

// bar 객체 생성
var bar = new Person('bar');
console.log(foo.country);
console.log(bar.country);
console.log(foo.constructor);
console.log(bar.constructor);
```

>Person(name) <br>
undefined <br>
Object() <br>
undefined <br>
korea <br>
Person(name) <br>
Object()

<br>

---

# 4.5.9 객체의 프로퍼티 읽기나 메서드를 실행할 때만 프로토타입 체이닝이 동작한다

객체의 특정 프로퍼티를 읽으려고 할 때, 프로퍼티가 해당 객체에 없는 경우 프로토타입 체이닝이 발생한다.

반대로 객체에 있는 특정 프로퍼티에 값을 쓰려고 한다면 이때는 프로토타입 체이닝이 일어나지 않는다. 자바스크립트는 객체에 없는 프로퍼티에 값을 쓰려고 할 경우 동적으로 객체에 프로퍼티를 추가하기 때문이다.

<4-44>

```jsx
// 프로토타입 체이닝과 동적 프로퍼티 생성
// Person() 생성자 함수
function Person(name) {
  this.name = name;
}

Person.prototype.country = 'Korea';

var foo = new Person('foo');
var bar = new Person('bar');
console.log(foo.country);
console.log(bar.country);
foo.country = 'USA';

console.log(foo.country);
console.log(bar.country);
```

>Korea <br>
Korea <br>
USA <br>
Korea