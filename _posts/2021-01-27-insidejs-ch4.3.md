---
title: "함수의 다양한 형태"
date: 2021-01-27 22:59
categories: [Javascript]
---

# [Inside Javascript] Ch4.3

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

<br>

# 4.3.1 콜백 함수

: 개발자는 단지 함수를 등록하기만 하고, 어떤 이벤트가 발생했거나 특정 시점에 도달했을 때 시스템에서 호출되는 함수

ex) 특정 함수의 인자로 넘겨서 코드 내부에서 호출되는 함수, 이벤트 핸들러 처리

** 이벤트 핸들러 처리
: 웹 페이지가 로드되거나 키보드가 입력되는 등의 DOM 이벤트가 발생할 경우, 브라우저는 정의된 DOM 이벤트에 해당하는 이벤트 핸들러를 실행 시킨다. 이러한 이벤트 핸들러에 콜백 함수가 등록했다면 콜백 함수는 이벤트가 발생할 때마다 브라우저에 의해 실행되게 된다.

<4-15>

```jsx
// window.onload 이벤트 핸들러 예제 코드

<!DOCTYPE html>
<html>
  <body>
    <script>
      // 페이지 로드 시 호출될 콜백 함수
      window.onload = function() {
        alert('This is the callback function.');
      };
    </script>
  </body>
</html>
```
![20210127-4.png](/assets/images/posts/2021-01-27/20210127-4.png)

<br>

---

# 4.3.2 즉시 실행 함수(immediate functions)

: 함수를 정의함과 동시에 바로 실행하는 함수

<4-16>

```jsx
// 즉시 실행 함수 예제 코드
(function (name) {
    console.log('This is the immediate function --> ' + name);
})('foo');
```

>This is the immediate unction —> foo

### 즉시 실행 함수를 만드는 방법

1. 함수 리터럴을 괄호()로 둘러싼다
2. 함수가 바로 호출된 수 있게 () 괄호 쌍을 추가(이때, 괄호 안에 값을 추가해 즉시 실행 함수의 인자로 넘길 수 있다.)

### 특성

- 같은 함수를 다시 호출할 수 없다
- 최초 한 번의 실행만을 필요로 하는 초기화 코드 부분등에 사용 가능
- jQuery와 같은 사바스크립트 라이브러리나 프레임워크 소스들에서 사용

### 자바스크립트의 변수 유효 범위 특성

- 변수를 선언할 경우 프로그램 전체에서 접근할 수 있는 전역 유효 범위를 가지게 된다.
- 함수 내부에서 정의된 매개변수와 변수들은 함수 코드 내부에서만 유효할 뿐 함수 밖에서는 유효하지 않다. = 함수 외부의 코드에서 함수 내부의 변수를 액세스하는 게 불가능하다

<br>

---

# 4.3.3 내부 함수(inner function)

: 자바스크립트의 기능을 보다 강력하게 해주는 클로저를 생성하거나 부모 함수 코드에서 외부에서의 접근을 막고 독립적인 헬퍼 함수를 구현하는 용도 등으로 사용한다.

<4-18>

```jsx
// 내부 함수 예제 코드
// parent() 함수 정의
function parent() {
    var a = 100;
    var b = 200;

    // child() 내부 함수 정의
    function child() {
        var b = 300;

        console.lod(a);
        console.log(b);
    }
    child();
}
 parent();
 child();
```

>100 <br>
300 <br>
Uncaught ReferenceError: child is not defined

### 내부 함수에서는 자신을 둘러싼 부모 함수의 변수에 접근이 가능하다

: 스코프 체이닝 때문

### 내부 함수는 일반적으로 자신이 정의된 부모 함수 내부에서만 호출이 가능하다

: 자바스크립트의 함수 스코핑 때문. 즉, 함수 내부에 선언된 변수는 함수 외부에서 접근이 불가능하다

<br>

부모 함수에서 내부 함수를 외부로 리턴하면, 부모 함수 밖에서도 내부 함수를 호출하는 것이 가능하다.

<4-19>

```jsx
// 함수 스코프 외부에서 내부 함수 호출하는 예제 코드
function parent() {
    var a = 100;
    // child() 내부 함수
    var child = function() {
        console.log(a);
    }

    // child() 함수 반환
    return child;
}

var inner = parent();
inner();
```

>100

<br>

---

# 4.3.4 함수를 리턴하는 함수

: 함수도 일급 객체이므로 일반 값처럼 함수 자체를 리턴할 

<4-20>

```jsx
// 자신을 재정의하는 함수 예제 코드
// self() 함수
var self = function() {
    console.log('a');
    return function () {
        console.log('b')
        ;
    }
}
self = self();
self();
```

>a <br>
b