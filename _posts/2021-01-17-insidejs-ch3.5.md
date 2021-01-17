---
title: "배열"
date: 2021-01-17 20:55
categories: [Javascript]
---

# [Inside Javascript] Ch3.5

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

# 3.5.1 배열 리터럴

: 자바스크립트에서 새로운 배열을 만드는 데 사용하는 표기법, 대괄호([])를 사용

<예제 3-13>

```jsx
// 배열 리터럴을 통한 배열 생성
var colorArr = ['orange', 'yellow', 'blue', 'green', 'red'];;
console.log(colorArr[0]);
console.log(colorArr[1]);
console.log(colorArr[4]);
```

orange
yellow
red

배열 리터럴에서는 각 요소의 값만을 포함한다. 배열은 해당 프로퍼티에 접근하기 위해 대괄호 내에 접근하고자 하는 원소에 배열 내 위치 인덱스값을 넣어서 접근한다. 배열 내의 첫 번째 원소는 인덱스 0부터 시작한다.

***
# 3.5.2 배열의 요소 생성

배열은 동적으로 배열 원소를 추가할 수 있다. 특히 자바스크립트 배열의 경우는 아무 인덱스 위치에나 값을 동적으로 추가할 수 있다.

<예제 3-14>

```jsx
// 배열 요소의 동적 생성

// 빈 배열
var emptyArr = [];
console.log(emptyArr[0]);

// 배열 요소 동적 생성
emptyArr[0] = 100;
emptyArr[3] = 'eight'
emptyArr[7] = true;
console.log(emptyArr);
console.log(emptyArr.length);
```

>undefined<br>
[ 100, <2 empty items>, 'eight', <3 empty items>, true ]
8

배열 리터럴에서 대괄호만을 사용할 경우, 빈 배열이 생성된다. 요소가 없는 빈 배열은 배열 원소에 접근해도 값이 없는 undefined 값이 출력된다. 

배열의 요소는 숫자나 문자열 같은 기본 타입의 값들을 포함해서, 객체나 함수, 배열 등과 같이 자바스크립트의 모든 데이터 타입을 포함할 수 있다.

자바스크립트는 배열의 크기를 현재 배열의 인덱스 중 가장 큰 값을 기준으로 정한다.

값이 할당되지 않은 인덱스 요소는 undefined 값을 기본으로 가진다. 배열의 원소 개수는 length 프로퍼티를 출력하면 알 수 있다.

***
# 3.5.3 배열의 length 프로퍼티

length 프로퍼티는 배열의 원소 개수를 나타내지만, 실제로 배열에 존재하는 원소 개수와 일치하는 것은 아니다. length 프로퍼티는 배열 내에 가장 큰 인덱스에 1을 더한 값이다. 때문에 배열의 가장 큰 인덱스값이 변하면 length 값 또한 자동으로 그에 맞춰 변경된다.

<예제 3-15>

```jsx
// 배열의 length 프로퍼티 변경
var arr = [];
console.log(arr.length);

arr[0] = 0;
arr[1] = 1;
arr[2] = 2;
arr[100] = 100;
console.log(arr.length);
```

>0<br>
101

배열 리터럴로 생성한 배열은 최초에 빈 배열이다. 때문에 length 프로퍼티값은 0이 된다. 그리고 동저긍로 배열 원소에 값을 저장할수록 가장 큰 인덱스값의 length 값이 늘어나는 것을 확인할 수 있다. 

<예제 3-16>

```jsx
// 배열 length 프로퍼티의 명시적 변경
var arr = [0, 1, 2];
console.log(arr.length);

arr.length = 5;
console.log(arr);

arr.length = 2;
console.log(arr);
console.log(arr[2]);
```

> 3<br>
[ 0, 1, 2, <2 empty items> ]<br>
[ 0, 1 ]<br>
undefined

***
## 3.5.3.1 배열 표준 메서드와 length 프로퍼티

자바스크립트는 배열에서 사용 가능한 다양한 표준 메서드를 제공한다. 이러한 배열 메서드는 length 프로퍼티를 기반으로 동작하고 있다.

`push()`

: 인스로 넘어온 항목을 배열의 끝에 추가하는 자바스크립트 표준 배열 메서드. 이 메서드는 배열의 현재 length 값의 위치에 새로운 원소값을 추가한다. 배열의 length 프로퍼티는 '현재 배열의 맨 마지막 원소의 인덱스+1'을 의미하므로 결국 length 프로퍼티가 가리키는 인덱스에 값을 저장하는 것은 배열의 끝에 값을 추가하는 것과 같은 결과가 되기 때문이다.

<예제 3-17>

```jsx
// push() 메서드와 length 프로퍼티
// arr 배열 생성
var arr = ['zero', 'one', 'two'];

// push() 메서드 호출
arr.push('three');
console.log(arr);

// length 값 변경 후, push() 메서드 호출
arr.length = 5;
arr.push('four');
console.log(arr);
```

>[ 'zero', 'one', 'two', 'three' ]<br>
[ 'zero', 'one', 'two', 'three', <1 empty item>, 'four' ]

***
# 3.5.4 배열과 객체

자바스크립트에서는 배열 역시 객체다. 하지만 배열은 일반 객체와 약간 차이가 있다. 

<예제 3-18>

```jsx
// 배열과 객체의 유사점과 차이점

// colorsArray 배열
var colorsArray = ['orange', 'yellow', 'green'];
console.log(colorsArray[0]);
console.log(colorsArray[1]);
console.log(colorsArray[2]);

// colorsObj 객체
var colorsObj = {
  '0': 'orange',
  '1': 'yellow',
  '2': 'green'
};
console.log(colorsObj[0]);
console.log(colorsObj[1]);
console.log(colorsObj[2]);

// typeof 연산자 비교
console.log(typeof colorsArray);  // not array
console.log(typeof colorsObj);

// length 프로퍼티
console.log(colorsArray.length);
console.log(colorsObj.length);

// 배열 표준 메서드
colorsArray.push('red');
colorsObj.push('red');
```

>TypeError: colorsObj.push is not a function
    at /script.js:29:11orange <br>
yellow<br>
green<br>
orange<br>
yellow<br>
green<br>
object<br>
object<br>
3<br>
undefined

1. 배열과 객체 생성

자바스크립트 엔진은 [ ] 연산자 내에 숫자가 사용될 경우, 해당 숫자를 자동으로 문자열 형태로 바꿔준다.

2. typeof 연산자 비교

typeof 연산 결과는 배열과 객체가 모두 object라는 것을 기억하자. 즉, 자바스크립트도 배열을 객체라고 생각한다는 것이다. 

3. length 프로퍼티 존재 여부

일반 객체는 length 프로퍼티가 존재하지 않는다.

4. 배열 표준 메서드 호출 여부

일반 객체는 push()와 같은 표준 배열 메서드를 사용할 수 없다. 객체 리터럴 방식으로 생성한 객체의 경우, 객체 표준 메서들르 저장하고 있는 Object.prototype 객체가 프로토타입이다. 반면에 배열의 경우 Array.prototype 객체가 부모 객체인 프로토타입이 된다. 그리고 Array.prototype 객체의 프로토타입은 Object.prototype 객체가 된다. 

<예제 3-19>

```jsx
// 배열의 프로토타입과 객체의 프로토타입 비교
 var emptyArray = [];
 var emptyObj = {};

 console.dir(emptyArray.__proto__);
 console.dir(emptyObj.__proto__);
```

![20210117155628.png](/assets/images/posts/2021-01-17/20210117155628.png)

***
# 3.5.5 배열의 프로퍼티 동적 생성

배열도 자바스크립트 객체이므로, 인덱스가 숫자인 배열 원소 이외에도 객체처럼 동적으로 프로퍼티를 추가할 수 있다.

<예제 3-20>

```jsx
// 배열의 동적 프로퍼티 생성

// 배열 생성
var arr = ['zero', 'one', 'two'];
console.log(arr.length);

// 포로퍼티 동적 추가
arr.color = 'blue';
arr.name = 'number_array';
console.log(arr.length);

// 배열 원소 추가
arr[3] = 'red';
console.log(arr.length);

// 배열 객체 출력
console.dir(arr);
```

>3<br>
3<br>
4<br>
[ 'zero', 'one', 'two', 'red', color: 'blue', name: 'number_array' ]

배열의 length 프로퍼티는 배열 원소의 가장 큰 인덱스가 변했을 경우만 변경된다.

배열도 객체처럼 'key: value' 형태로 배열 원소 및 프로퍼티 등이 있다.

***
# 3.5.6 배열의 프로퍼티 열거

배열도 객체이므로 for in 문을 사용해서 배열 내의 모든 프로퍼티를 열거할 수 있지만, 이렇게 되면 불필요한 프로퍼티가 출력될 수 있으므로 되도록 for 문을 사용하는 것이 좋다.

<예제 3-21>

```jsx
// 배열의 프로퍼티 열거
// 배열의 동적 프로퍼티 생성

// 배열 생성
var arr = ['zero', 'one', 'two'];
console.log(arr.length);

// 포로퍼티 동적 추가
arr.color = 'blue';
arr.name = 'number_array';
console.log(arr.length);

// 배열 원소 추가
arr[3] = 'red';
console.log(arr.length);

// 배열 객체 출력
console.dir(arr);

for (var prop in arr) {
  console.log(prop, arr[prop]);
}

for (var i=0; i<arr.length; i++) {
  console.log(i, arr[i]);
}
```

>0 zero<br>
1 one<br>
2 two<br>
3 red<br>
color blue<br>
name number_array<br>
0 'zero'<br>
1 'one'<br>
2 'two'<br>
3 'red'<br>

***
# 3.5.7 배열 요소 삭제

<예제 3-22>

```jsx
// delete 연산자를 이용한 배열 프로퍼티 삭제

var arr = ['zero', 'one', 'two', 'three'];
delete arr[2];
console.log(arr);
console.log(arr.length);
```

> [ 'zero', 'one', <1 empty item>, 'three' ]<br>
4

배열도 객체이므로, 배열 요소나 프로퍼티를 삭제하는 데 delete 연산자를 사용할 수 있다. 하지만, delete 연산자는 해당 요소의 값을 undefined로 설정할 뿐 원소 자체를 삭제하지는 않는다. 때문에 보통 배열에서 요소들을 완전히 삭제할 경우 자바스크립트에서는 splice() 배열 메서드를 사용한다.

`splice(start, deleteCount, item...)`

- start: 배열에서 시작 위치
- deleteCount: start에서 지정한 시작 위치부터 삭제할 요소의 수
- item: 삭제할 위치에 추가할 요소

***
# 3.5.8 Array() 생성자 함수

배열은 일반적으로 배열 리터럴로 생성하지만 배열 리터럴도 결국 자바스크립트 기본 제공 Array() 생성자 함수로 배열을 생성하는 과정을 단순화시킨 것이다. 생성자 함수로 배열과 같은 객체를 생성할 때는 반드시 new 연산자를 같이 써야 한다.

Array() 생성자 함수는 호출할 때 인자 개수에 따라 동작이 다르다.

- 호출할 때 인자가 1개이고, 숫자일 경우: 호출된 인자를 length로 갖는 빈 배열 생성
- 그외의 경우: 호출된 인자를 요소로 갖는 배열 생성

<예제 3-23>

```jsx
// delete 연산자를 이용한 배열 프로퍼티 삭제

var arr = ['zero', 'one', 'two', 'three'];

arr.splice(2, 1);
console.log(arr);
console.log(arr.length);
```

>[ 'zero', 'one', 'three' ]<br>
3

<예제 3-24>

```jsx
// Array() 생성자 함수를 통한 배열 생성

var foo = new Array(3);
console.log(foo);
console.log(foo.length);

var bar = new Array(1, 2, 3);
console.log(bar);
console.log(bar.length);
```
>[ <3 empty items> ]<br>
3<br>
[ 1, 2, 3 ]<br>
3

***
# 3.5.9 유사 배열 객체

: length 프로퍼티를 가진 객체

가장 큰 특징은 객체임에도 불구하고, 자바스크립트의 표준 배열 메서드를 사용하는 게 가능하다는 것이다. 


<예제 3-25>

```jsx
// 유사 배열 객체의 배열 메서드 호출

var arr = ['bar'];
var obj = {
  name: 'foo',
  length: 1
};

arr.push('baz');
console.log(arr);

obj.push('baz');
```

>TypeError: obj.push is not a function
    at /script.js:12:5 <br>
[ 'bar', 'baz' ]

apply() 메서드를 사용하면 객체지만 표준 배열 메서드를 활용하는 것이 가능하다. 

<예제 3-26>

```jsx
var arr = ['bar'];
var obj = { name: 'foo', length: 1 };

arr.push('baz');
console.log(arr);

Array.prototype.push.apply(obj, ['baz']);
console.log(obj);
```

>[ 'bar', 'baz' ]<br>
{ 1: 'baz', name: 'foo', length: 2 }