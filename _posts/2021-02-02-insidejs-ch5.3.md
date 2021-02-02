---
title: "[Javascript] 스코프 체인"
date: 2021-02-02 20:37
categories: [Javascript]
---

# [Inside Javascript] Ch5.3

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

<br>

## 스코프 체인

: 유효 범위를 나타내는 스코프가 [[scope]] 프로퍼티로 각 함수 객체 내에서 연결 리스트 형식으로 관리되는 것, 각 실행 컨텍스트의 변수 객체가 구성 요소인 리스트와 같음

- 각각의 함수는 [[scope]] 프로퍼티로 자신이 생성된 실행 컨텍스트의 스코프 체인을 참조
- 함수가 실행되는 순간 실행 컨텍스트가 만들어짐 ⇒ 이 실행 컨텍스트는 실행된 함수의 [[scope]] 프로퍼티를 기반으로 새로운 스코프 체인을 만듦

<br>

---

# 5.3.1 전역 실행 컨텍스트의 스코프 체인

<5-3>

```jsx
var var1 = 1;
var var2 = 2;
console.log(var1);
console.log(var2);
```

>1 <br>
2

전역 실행 컨텍스트 단 하나만 실행되고 있어 참조할 상위 컨텍스트가 없음 = 자신이 최상위에 위치하는 변수 객체
⇒ 이 변수 객체의 스코프 체인은 자기 자신만을 가짐 = 변수 객체의 [[scope]]는 변수 객체 자신을 가리킨다.

<br>

---

# 5.3.2 함수를 호출한 경우 생성되는 실행 컨텍스트의 스코프 체인

<5-4>

```jsx
var var1 = 1;
var var2 = 2;
function func() {
  var var1 = 10;
  var var2 = 20;
  console.log(var1);
  console.log(var2);
}
func();
console.log(var1);
console.log(var2);
```

>10 <br>
20 <br>
1 <br>
2

### 스코프체인 = 현재 실행 컨텍스트의 변수 객체 + 상위 컨텍스트의 스코프 체인

- 각 함수 객체는 [[scope]] 프로퍼티로 현재 컨텍스트의 스코프 체인을 참조한다.
- 한 함수가 실행되면 새로운 실행 켄텍스트가 만드렁지는데, 이 새로운 실행 컨텍스트는 자신이 사용할 스코프 체인을 다음과 같은 방법으로 만든다.
현재 실행되는 함수 객체의 [[scope]] 프로퍼티를 복사 → 새롭게 생성된 변수 객체를 해당 체인의 제일 앞에 추가

<5-5>

```jsx
var value = "value1";

function printFunc() {
  var value = "value2";

  function printValue() {
    return value;
  }

  console.log(printValue());
}

printFunc();
```

>value2

<5-6>

```jsx
var value = "value1";

function printValue() {
  return value;
}
function printFunc(func) {
  var value = "value2";
  console.log(func());
}
printFunc(printValue)
```

>value1

이렇게 만들어진 스코프 체인으로 식별자 인식(identifier resolution)이 이루어진다. 

1. 스코프 체인의 첫번째 변수 객체부터 시작한다.
2. 식별자와 대응되는 이름을 가진 프로퍼티가 있는지를 확인한다.
3. 함수를 호출할 때 스코프 체인의 가장 앞에 있는 객체가 변수 객체이므로, 이 객체에 있는 공식 인자, 내부 함수, 지역 변수에 대응되는지 먼저 확인
4. 첫 번째 객체에 대응되는 프로퍼티를 발견하지 못하면, 다음 객체로 이동하여 찾는다
5. 이런 식으로 대응되는 이름의 프로퍼티를 찾을 때까지 계속된다.
6. 여기서 this는 식별자가 아닌 키워드로 분류되므로, 스코프 체인의 참조 없이 접근할 수 있음