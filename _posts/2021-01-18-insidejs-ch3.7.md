---
title: "연산자"
date: 2021-01-18 20:40
categories: [Javascript]
---

# [Inside Javascript] Ch3.7

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

# 3.7.1 + 연산자

: 더하기 연산과 문자열 연결 연산을 수행한다. 두 연산자가 모두 숫자일 경우에만 더하기 연산이 수행되고, 나머지는 문자열 연결 연산이 이뤄진다.

<예제 3-28>

```jsx
// + 연산자 예제

var add1 = 1 + 2;
var add2 = 'my' + 'string';
var add3 = 1 + 'string';
var add4 = 'string' + 2;

console.log(add1);
console.log(add2);
console.log(add3);
console.log(add4);
```

>3<br>
mystring<br>
1string<br>
string2

<br>

***
# 3.7.2 typeof 연산자
![20210118003841.png](/assets/images/posts/2021-01-18/20210118003841.png)

<br>

***
# 3.7.3 ==(동등) 연산자와 ===(일치) 연산자

== 연산자: 비교하려는 피연산자의 타입이 다를 경우에 타입 변환을 거친 다음 비교

=== 연산자: 피연산자의 타입이 다를 경우에 타입을 변경하지 않고 비교

<예제 3-29>

```jsx
// ==(동등) 연산자와 ===(일치)연산자의 차이점
console.log(1 == '1');
console.log(1 === '1');
```

>true<br>
false

== 연산자의 비교는 타입 변환에 따른 잘못된 결과를 얻을 수 있으므로 === 연산자로 비교하기를 권장

<br>

# 3.7.4 !!연산자

: 피연산자를 불린값으로 변환

<예제 3-30>

```jsx
// !! 연산자 활용을 통한 불린값 변환
console.log(!!0);
console.log(!!1);
console.log(!!'string');
console.log(!!'');
console.log(!!true);
console.log(!!false);
console.log(!!null);
console.log(!!undefined);
console.log(!!{});
console.log(!![1, 2, 3]);
```

>false<br>
true<br>
true<br>
false<br>
true<br>
false<br>
false<br>
false<br>
true<br>
true

객체는 값이 비어있는 빈 객체라도 true로 변환됨