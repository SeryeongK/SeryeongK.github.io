---
title: "프로토타입"
date: 2021-01-17 16:33
categories: [Javascript]
---

# [Inside Javascript] Ch3.4

※ <인사이드 자바스크립트>(송형주, 고현준 지음)을 바탕으로 작성하였습니다. ※

자바스크립트의 모든 객체는 자신의 부모 역할을 하는 객체와 연결되어 있다. 그리고 이것은 마치 객체지향의 상속 개념과 같이 부모 객체의 프로퍼티를 마치 자신의 것처럼 쓸 수 있는 것 같은 특징이 있다. 자바스크립트에서는 이러한 부모 객체를 프로토타입 객체(짧게는 프로토타입)라고 부른다.

<예제 3-12>

```jsx
var foo = {
  name: 'foo',
  age: 30
};

console.log(foo.toString());

console.dir(foo);
```

![20210117155627.png](/assets/images/posts/2021-01-17/20210117155627.png)

>`obj.toString()` ⇒ A string representing the object

(reference: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString))

>`console.dir(object);`

: an interactive list of the properties of the specified JavaScript object

⇒ a hierarchcal listing with disclosure triangles that let you see the contents of child objects.

parameter: object(A JavaScript object whose properties should be output)

(reference: [https://developer.mozilla.org/en-US/docs/Web/API/Console/dir](https://developer.mozilla.org/en-US/docs/Web/API/Console/dir))

자바스크립트의 모든 객체는 자신의 프로토타입을 가리키는 [[Prototype]]라는 숨겨진 프로퍼티를 가진다. 크롬 브라우저에서는 __proto__가 바로 이 숨겨진 [[Prototype]] 프로퍼티를 의미한다.

객체를 생성할 때 결정된 프로토타입 객체는 임의의 다른 객체로 변경하는 것도 가능하다. 즉, 부모 객체를 동적으로 바꿀 수도 있는 것이다.