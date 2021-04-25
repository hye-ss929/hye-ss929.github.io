---
layout: post
title: Strict Mode
date: 2021-04-26 12:54 +0800
tags: [JavaScript]
excerpt: Strict MOde
---

# Strict Mode

- ES5부터 추가
- 자바스크립트 언어의 문법을 보다 엄격히 적용하여 기존에는 무시되던 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킴

### Strict Mode의 적용

- 전역의 선두 또는 함수의 선두에 `'use strict';`를 추가
  - 전역의 선두에 추가하면 스크립트 전체에 strict mode가 적용된다.

```js
"use strict";

function foo() {
  x = 10; // ReferenceError: x is not defined
}
console.log(foo());
```

- 함수에 Strict Mode를 적용하기 위해 함수 처음에 `'use strict';`추가

```js
function foo() {
  "use strict";

  x = 10; // ReferenceError: x is not defined
}
foo();
```

### Strict Mode의 특징

- 기존에 조용히 무시되던 에러들을 throwing 함
- 실수로 글로벌 변수를 생성하는 것을 불가능하게 함
- 전체 스크립트 또는 부분 함수에 적용 가능
- {} 괄호로 묶여진 block문, context에 적용되지 않음
- JavaSCript 엔진의 최적화 작업을 어렵게 만드는 실수를 바로 잡음. 종종 strict Mode(엄격 모드)는 sloppy mode(느슨한 모드)의 동일한 코드보다 더 빨리 작동하도록 만들어짐
- strict Mode는 ECMAScrpt의 차기 버전들에서 정의될 문법을 금지
  - strict Mode에서의 식별자 후보들은 예약어(implements, interface, let, package, private, protected, public, static, yield)가 됨
  - 그럼, strict Mode에서는 이 예약어와 똑같은 이름을 사용하거나, 변수명 또는 아규먼트명으로도 사용할 수 없음

```js
"use strict";

// 쓸 수 없는 프로퍼티에 할당
var undefined = 5; // TypeError 발생
var Infinity = 5; // TypeError 발생

// 쓸 수 없는 프로퍼티에 할당
var obj1 = {};
Object.defineProperty(obj1, "x", { value: 42, writable: false });
obj1.x = 9; // TypeError 발생

// getter-only 프로퍼티에 할당
var obj2 = {
  get x() {
    return 17;
  },
};
obj2.x = 5; // TypeError 발생

// 확장 불가 객체에 새 프로퍼티 할당
var fixed = {};
Object.preventExtensions(fixed);
fixed.newProp = "ohai"; // TypeError 발생
```

> 출처 : [MDM](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Strict_mode)
