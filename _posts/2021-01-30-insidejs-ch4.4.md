---
title: "함수 호출과 this"
date: 2021-01-30 14:43
categories: [Javascript]
---


# [Inside Javascript] Ch4.4

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

<br>

# 4.4.1 argument 객체

자바스크립트에서는 함수를 호출할 때, 함수 형식에 맞춰 인자를 넘기지 않더라도 에러가 발생하지 않는다. 

<4-21>

```jsx
// 함수 형식에 맞춰 인자를 넘기지 않더라도 함수 호출이 가능함을 나타내는 예제 코드
function func(arg1, arg2) {
    console.log(arg1, arg2);
}

func();
func(1);
func(1, 2);
func(1, 2, 3);
```

>undefined undefined <br>
1 undefined <br>
1 2 <br>
1 2 

- 정의된 함수의 인자보다 적게 함수를 호출했을 경우: 넘겨지지 않은 인자에는 **undefined 값**이 할당
- 정의된 인자 개수보다 많게 함수를 호출했을 경우: 에러가 발생하지 않고, **초과된 인수는 무시**

### argument 객체

: 함수를 호출항 때 넘긴 인자들이 배열 형태로 저장된 객체

- 런타임 시에 호출된 인자의 개수를 확인하고 이에 따라 동작을 다르게 해주는 것을 가능하게 함
- 자바스크립트에서 함수를 호출할 때 인수들과 함께 암묵적으로 함수 내부로 전달됨
- 실제 배열이 아닌 **유사 배열 객체**

<4-22>

```jsx
// arguments 객체 예제 코드
// add() 함수
function add(a, b) {
    // arguments 객체 출력
    console.dir(arguments);
    return a + b;
}

console.log(add(1));
console.log(add(1, 2));
console.log(add(1, 2, 3));
```

![20210130-1.png](/assets/images/posts/2021-01-30/20210130-1.png)


### arguments 객체의 구성

- 함수를 호출할 때 넘겨진 인자(배열 형태): 함수를 호출할 때 첫 번째 인자는 0번 인덱스, 두 번째 인자는 1번 인덱스, ...
- length 프로퍼티: 호출할 때 넘겨진 인자의 개수를 의미
- callee 프로퍼티: 현재 실행 중인 함수의 참조값(예제에서는 add() 함수)

** arguments 객체는 length 프로퍼티가 있으므로 배열과 유사하게 동작하지만, 배열은 아니므로 배열 메서드를 사용할 수 없다

<br>

---

# 4.4.2 호출 패턴과 this 바인딩

자바스크립트에서 함수를 호출할 때 기존 매개변수로 전달되는 인자값에 더해, arguments 객체 및 this 인자가 함수 내부로 암묵적으로 전달된다.

<br>

## 4.4.2.1 객체의 메서드 호출할  때 this 바인딩

** 메서드: 객체의 프로퍼티가 함수일 경우, 해당 함수

메서드를 호출할 때 메서드 내부 코드에서 사용된 this는 **해당 메서드를 호출한 객체**로 바인딩된다.

<4-23>

```jsx
// 메서드 호출 사용 시 this 바인딩
// myObject 객체 생성
var myObject = {
    name: 'foo',
    sayName: function() {
        console.log(this.name);
    }
};

// otherObject 객체 생성
var otherObject = {
    name: 'bar'
};

// otherObject.sayNanme() 메서드
otherObject.sayName = myObject.sayName;

// sayName() 메서드 호출
myObject.sayName();
otherObject.sayName();
```

>foo <br>
bar

<br>

## 4.4.2.2 함수를 호출할 때 this 바인딩

자바스크립트에서는 함수를 호출하면, 해당 함수 내부 코드엣 사용된 **this는 전역 객체에 바인딩**된다. 브라우저에서 자바스크립트를 실행하는 경우 전역 객체는 **window 객체**가 된다.

<4-24>

```jsx
// 전역 객체와 전역 변수의 관계를 보여주는 예제 코드

var foo = "I'm foo";    // 전역 변수 선언
console.log(foo);
console.log(window.foo);
```

>foo <br>
foo

<4-25>

```jsx
// 함수를 호출할 때 this 바인딩을 보여주는 예제 코드
var test = 'This is test';
console.log(window.test);

// sayFoo() 함수
var sayFoo = function() {
    console.log(this.test); // sayFoo() 함수 호출 시 this는 전역 객체에 바인딩된다.
};

sayFoo();
```

> This is test <br>
This is test

함수 호출에서의 this  바인딩 특성은 내부 함수(inner function)를 호출했을 경우에도 그래도 적용

<4-26>

```jsx
// 내부 함수의 this 바인딩 동작을 보여주는 예제 코드
// 전역 변수 value 정의
var value = 100;

// myObject 객체 생성
var myObject = {
    value: 1,
    func1: function() {
        this.value += 1;
        console.log('func1() called. this.value : ' + this.value);

      // func2() 내부 함수
      func2 = function() {
        this.value += 1;
          console.log('func2() called. this.value : ' + this.value);

        // func3() 내부 함수
        func3 = function() {
        this.value += 1;
        console.log('func1() called. this.value : ' + this.value);
      }
      func3();  // func3() 내부 함수 호출
    }
    func2();  //func2() 내부 함수 호출
  }
};
myObject.func1(); // func1() 메서드 호출
```

>func1() called. this.value : 2 <br>
func1() called. this.value : 101 <br>
func1() called. this.value : 102

이렇게 내부 함수가 this를 참조하는 자바스크립트의 함계를 극복하려면 부모 함수의 this를 내부 함수가 접근 간으한 다른 변수에 저장하는 방법이 사용된다. 관례상 this 값을 저장하는 변수의 이름을 that이라고 짓는다. 

<4-27>

```jsx
// 내부 함수의 this 바인딩 문제를 해결한 예제 코드
// 내부 함수 this 바인딩

var value = 100;
var myObject = {
    value 1,
    func1: function() {
        var that = this;

        this value += 1;
        console.log('func1() called. this.value : ' + this.value);

        func2 = function() {
            that.value += 1;
            console.log('func2() called. this.value : ' + that.value);
            
            func3 = function () {
                that.value += 1;
                console.log('func3() called. this.value : ' + that.value);
            }
            func3();
        }
        func2();
    }
};

myObject.func1()    // func1 메서드 호출
```

>func1() called. this.value : 2 <br>
func1() called. this.value : 3 <br>
func1() called. this.value : 4

<br>

## 4.4.2.3 생성자 함수를 호출할 때 this 바인딩

### 자바스크립트 객체를 생성하는 방법 2가지

1. 객체 리터럴 방식
2. 생성자 함수를 이용하는 방식

기존 함수에 new 연산자를 붙여서 호출하면 해당 함수는 자바스크립트의 객체를 생성하는 역할을 하는 생성자 함수로 동작한다. 대부분의 자바스크립트 스타일 가이드에서는 특정 함수가 생성자 함수로 정의되어 있음을 알리려고 함수 이름의 첫 문자를 대문자로 쓰기를 권하고 있다. 

### new 연산자로 자바스크립트 함수를 생성자로 호출 → 생성자 함수가 동작하는 방식

1. 빈 객체 생성 및 this 바인딩
생성자 함수 코득 실행되기 전 생성자 함수가 새로 생성하는 빈 객체가 생성된다. 이 객체는 this로 바인딩된다. 따라서 이후 생성자 함수의 코드 내부에서 사용된 this는 이 빈 객체를 가리킨다. 하지만 여기서 생성된 객체는 엄밀히 마라면 빈 객체는 아니다. 부모인 프로토타입 객체와 연결되어 있어 이를 통해 부모 객체의 프로퍼티나 메서드를 마치 자신의 것처럼 사용할 수 있기 때문이다. 이렇게 생성자 함수가 생성한 객체는 자신을 생성자 함수의 prototype 프로퍼티가 가리키는 객체를 자신의 프로토타입 객체로 설정한다. 
2. this를 통한 프로퍼티 생성
함수 코드 내부에서 this를 사용해서, 앞에서 생성된 빈 객체에 동적으로 프로퍼티나 메서드를 생성할 수 있다.
3. 생성된 객체 리턴
특별하게 리턴문이 없을 경우, this로 바인딩된 새로 생성한 객체가 리턴된다. 이것은 명시적으로 this를 리턴해도 결과는 같다. (cf) 일반 함수를 호출할 때 리턴값이 명시되어 있지 않으면 undefined가 리턴된다.) 하지만 리턴값이 새로 생성한 객체(this)가 아닌 다른 객체를 반환하는 경우는 생성자 함수를 호출했다고 하더라도 this가 아닌 해당 객체가 리턴된다.

<4-28>

```jsx
// 생성자 함수의 동작 방식

// Person() 생성자 함수
var Person = function (name) {
  // 함수 코드 실행 전
  this.name = name;
  // 함수 리턴
};

// foo 객체 생성
var foo = new Person('foo');
console.log(foo.name);
```

>foo

<4-29>

```jsx
// 객체 생성 두 가지 방법(객체 리터럴 vs 생성자 함수)
// 객체 리터럴 방식으로 foo 객체 생성
var foo = {
  name: 'foo',
  age: 35,
  gender: 'man'
};
console.dir(foo);

// 생성자 함수
function Person(name, age, gender, position) {
  this.name = name;
  this.age = age;
  this.gender = gender;
}

// Person 생성자 함수를 이용해 bar 객체, baz 객체 생성
var bar = new Person('bar', 33, 'woman');
console.dir(bar);

var baz = new Person('baz', 25, 'woman');
console.dir(baz);
```

![20210130-2.png](/assets/images/posts/2021-01-30/20210130-2.png)


### 객체 리터럴 방식과 생성자 함수를 통한 객체 생성 방식의 차이

- 객체 리터럴 방식으로 생성된 객체는 같은 형태의 객체를 재생성할 수 없다
- 프로토타입 객체(__proto__ 프로퍼티)
객체 리터럴 방식: 자신의 프로토타입 객체가 Object(Objec.prototype)
생성자 함수 방식: Person(Person.prototye)

<br>

**자바스크립트 객체 생성 규칙**

자바스크립트 객체는 자신을 생성한 생성자 함수의 prototype 프로터피가 가리키는 객체를 자신의 프로토타입 객체로 설정한다. 객체 리터럴 방식에서는 객체 생성자 함수는 Object()이며, 생성자 함수 방식의 경우는 생성자 함수 자체, Person()이므로 두 가지 방식이 다른 프로토타입 객체가 있는 것이다. 

### 생성자 함수를 new를 붙이지 않고 호출할 경우

객체 생성을 목적으로 작성한 생성자 함수를 new 없이 호출하거나 일방 함수를 new를 붙여서 호출할 경우 코드에서 오류가 발생할 수 있다. 그 이유는 일반 함수 호출과 생성자 함수를 호출할 때 this 바인딩 방식이 다르기 때문이다. 일반 함수 호출의 경우는 this가 window 전역 객체에 바인딩되는 반면에, 생성자 함수 호출의 경우 this는 새로 생성되는 빈 객체에 바인딩되기 때문이다. 

<4-30>

```jsx
// new를 붙이지 않고 생성자 함수 호출 시의 오류

// 생성자 함수
function Person(name, age, gender, position) {
  this.name = name;
  this.age = age;
  this.gender = gender;
}

var qux = Person('qux', 20, 'man');
console.log(qux);

console.log(window.name);
console.log(window.age);
console.log(window.gender);
```

>undefined <br>
qux <br>
20 <br>
man

** 자바스크립트에서는 읿반 함수와 생성자 함수의 구분이 별도로 없으므로, 일반적으로 생성자 함수로 사용할 함수는 첫 글자를 대문자로 표기하는 네이밍 규칙을 권장

<br>

## 4.4.2.4 call과 apply 메서드를 이용한 명시적인 this 바인딩

- call() 메서드는 apply() 메서드와는 기능이 같고 단지 넘겨받는 인자의 형식만 다름
- apply() 메서드를 호출하는 주체는 함수
- apply() 메서드도 this를 바인딩할 뿐 결국 본질적인 기능은 **함수 호출**

`function.apply(thisArg, argArray)`

- thisArg: apply() 메서드를 호출한 함수 내부에서 사용한 this에 바인딩할 객체를 가리킴, 첫 번째 인자로 넘긴 객체가 thsi로 명시적으로 바인딩됨
- argArray: 함수를 호출할 때 넘길 인자들의 배열

: 두 번째 인자인 arrArray 배열을 자신을 호출한 함수의 인자로 사용하되, 이 함수 내부에서 사용된 this는 첫 번째 인자인 thsiArg 객체로 바인딩해서 함수를 호출하는 기능을 하는 것이다.

`function.call(thisArg, prop1, prop2, ...)`

<4-31>

```jsx
// apply() 메서드를 이용한 명시적인 this 바인딩
// 생성자 함수
function Person(name, age, gender) {
  this.name = name;
  this.age = age;
  this.gender = gender;
}

// foo 빈 객체 생성
var foo = {};
// poo 빈 객체 생성
var poo = {};

// apply() 메서드 호출
Person.apply(foo, ['foo', 30, 'man']);

// call() 메서드 호출
Person.call(poo, 'poo', 30, 'man');

console.dir(foo);
console.dir(poo);
```

![20210130-3.png](/assets/images/posts/2021-01-30/20210130-3.png)


apply() 메서드: `object.apply(varName, [...])`

call() 메서드: `object.call(varNamr, ...)`

- 장점: this를 원하는 값을 명시적으로 매핑해서 특정 함수나 메서드를 호출할 수 있다.
- 용도: arguments 객체와 같은 유사 배열 객체에서 배열 메서드를 사용하는 경우

<br>

<4-32>

```jsx
// apply() 메서드를 활용한 arguments 객체의 배열 표준 메서드 slice() 활용 코드
function myFunction() {
  console.dir(arguments);

  // arguments.shift() 에러 발생

  // arguments 객체를 배열로 변환
  var args = Array.prototype.slice.apply(arguments);
  console.dir(args);
}

myFunction(1, 2, 3);
```

{ 0: 1, 1: 2, 2: 3 }
[ 1, 2, 3 ]

![20210130-4.png](/assets/images/posts/2021-01-30/20210130-4.png)


`Array.prototype.slice.apply(arguments)`: Array.prototype.slice() 메서드를 호출해라. 이때 this는 arguments 객체로 바인딩해라

`slice(start, end)` 메서드: 이 메서드를 호출한 배열의 start 인덱스에서 end-1 인덱스까지 복사한 배열을 리턴한다. end 인자를 지정하지 않을 경우 기본값은 배열의 length 값이다. slice() 메서드에 아무 인자도 넘기지 않을 경우는 전체 배열이 복사된다.

<4-33>

```jsx
// slice() 메서드 사용 예제

var arrA = [1, 2, 3];
var arrB = arrA.slice(0);
var arrC = arrA.slice();
var arrD = arrA.slice(1);
var arrE = arrA.slice(1, 2);

console.log(arrA);
console.log(arrB);
console.log(arrC);
console.log(arrD);
console.log(arrE);
```

>[ 1, 2, 3 ] <br>
[ 1, 2, 3 ] <br>
[ 1, 2, 3 ] <br>
[ 2, 3 ] <br>
[ 2 ]

<br>

---

# 4.4.3 함수 리턴

**자바스크립트 함수는 항상 리턴값을 반환한다.** 특히, return 문을 사용하지 않았더라도 다음의 규칙으로 항상 리턴값을 전달하게 된다.

## 4.4.3.1 규칙 1) 일반 함수나 메서드는 리턴값을 지정하지 않을 경우, undefined 값이 리턴된다.

<4-34>

```jsx
// return문 없는 일반 함수의 리턴값 확인
// niReturnFunc() 함수
var noReturnFunc = function () {
  console.log('This function has no reutrn statement.');
};

var result = noReturnFunc();
console.log(result);
```

> This function has no return statement. <br>
undefined

<br>

## 4.4.3.2 규칙 2) 생성자 함수에서 리턴값을 지정하지 않을 경우 생성된 객체가 리턴된다.

<4-35>

```jsx
// 생성자 함수에서 명시적으로 객체를 리턴했을 경우
// Person() 생성자 함수
function Person(name, age, gender) {
  this.name = name;
  this.age = age;
  this.gender = gender;

  // 명시적으로 다른 객체 반환
  return {name:'bar', age:20, gender:'woman'};
}

var foo = new Person('foo', 30, 'man');
console.dir(foo);
```

![20210130-5.png](/assets/images/posts/2021-01-30/20210130-5.png)


- 생성자 함수의 리턴값을 새로 생성한 객체가 아니라, 객체 리터럴 방식의 특정 객체로 지정한 경우 new 연산자로 생성자 함수를 호출해서 새로운 객체를 생성하더라도, 리턴값에서 명시적으로 넘긴 객체나 배열이 리턴된다.
- 생성자 함수의 리턴값으로 넘긴 값이 객체가 아닌 불린, 숫자, 문자열의 경우는 이러한 리턴값을 무시하고 this로 바인딩된 객체가 리턴된다.

<br>

<4-36>

```jsx
// 생성자 함수에서 명시적으로 기본 타입(불린, 숫자, 문자열) 값을 리턴했을 경우
// Person() 생성자 함수
function Person(name, age, gender) {
  this.name = name;
  this.age = age;
  this.gender = gender;

  return 100;
}

var foo = new Person('foo', 30, 'man');
console.dir(foo);
```

>Person { name: 'foo', age: 30, gender: 'man' }