# [Inside Javascript] Ch3.3 참조 타입의 특성

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

객체는 자바스크립트에서 참조 타입이라고 부른다. 기본 타입인 숫자, 문자열, 불린값, null, undefined 5가지를 제외한 모든 값(배열이나 함수 등등)은 객체다. 객체의 모든 연산은 실제 값이 아닌 참조값으로 처리된다.

<예제 3-9>

```jsx
// 동일한 객체를 참조하는 두 변수 objA와 objB
var objA = {
  val : 40
};
var objB = objA;

console.log(objA.val);
console.log(objB.val);

objB.val = 50;
console.log(objA.val);
console.log(objB.val);
```

>40<br>
40<br>
50<br>
50

>objA 변수는 객체 자체를 저장하고 있는 것이 아니라 생성된 객체를 가리키는 참조값을 저장하고 있다.

***
# 3.3.1 객체 비교

동등 연산자(==)를 사용하여 두 객체를 비교할 떄도 객체의 프로퍼티값이 아닌 참조값을 비교한다는 것에 주의해야 한다.

<3-10>

```jsx
var a = 100;
var b = 100;

var objA = { value: 100 };
var objB = { value: 100 };
var objC = objB;
console.log(a == b);
console.log(objA == objB);
console.log(objB == objC)
```

>true<br>
false<br>
true

>기본 타입의 경우는 값 자체를 비교해서 일치여부를 판단하지만, 객체와 같은 참조 타입의 경우는 참조값이 같아야 true가 된다.

***
# 3.3.2 참조에 의한 함수 호출 방식

### 기본 타입: 값에 의한 호출(Call by Value) 방식

함수를 호출할 때 인자로 기본 타입의 값을 넘길 경우, 호출된 함수의 매개변수로 복사된 값이 전달됨

### 참조 타입(객체 등): 참조에 의한 호출(Call by Reference) 방식

함수를 호출할 떄 인자로 참조 타입인 객체를 전달할 경우, 객체의 프로퍼티값이 함수의 매개변수로 복사되지 않고, 인자로 넘긴 객체의 참조값이 그대로 함수 내부로 전달됨

<3-11>

```jsx
var a = 100;
var objA = { value: 100 };

function changeArg(num, obj) {
  num = 200;
  obj.value = 200;

  console.log(num);
  console.log(obj);
}

changeArg(a, objA);

console.log(a);
console.log(objA);
```

>200<br>
{ value: 200 }<br>
100<br>
{ value: 200 }