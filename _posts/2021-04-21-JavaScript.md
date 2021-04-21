---
layout: post
title: JavaScript - 실행 컨텍스트
date: 2021-04-21
tags: [JavaScript]
excerpt: JavaScript - 실행 컨텍스트!
---

# JavaScript - 실행 컨텍스트

"실행할 코드에 제공할 환경 정보들을 모아놓은 객체로, 자바스크립트의 동적 언어로서의 성격을 가장 잘 파악할 수 있는 개념"

## 스택(Stack)

- 출입구가 하나뿐인 깊은 우물 같은 데이터 구조
  ![](https://images.velog.io/images/hyehye/post/784b637d-d28f-4311-9670-afd86384a55c/stack.webp)
- 비어있는 순서대로 데이터 1,2,3를 저장(Push)했다면, 꺼낼때는 반대로 3,2,1의 순서로 꺼내는 것(Pop).

## 큐(Queue)

- 양쪽이 모두 열려있는 파이프 구조
- 종류에 따라 양쪽 모두 입력과 출력이 가능한 큐도 있으나, 보통은 한쪽은 입력만, 다른 한쪽은 출력만을 담당하는 구조
  ![](https://images.velog.io/images/hyehye/post/11bb09d9-f9f9-4998-b754-b02f35d74986/%E1%84%8F%E1%85%B2.png)

---

## 실행 컨텍스트의 동작

- 동일한 환경에 있는 코드들을 실행할 때 필요한 환경 정보들을 모아 컨텍스트에 구성
- 컨텍스트들을 순서대로 **콜 스택(Call Stack)** 에 쌓아올림
- 가장 위에 쌓여있는 컨텍스트와 관련 있는 코드들을 실행
- 전체 코드의 환경과 순서를 보장
  👉🏻 콜 스택(Call Stack) : 자바스크립트 엔진이 구동되면서 실행 중인 코드를 추적하는 공간
- 함수(Function)의 호출(Call)을 기록하는 스택(Stack)자료구조

## 실행 컨텍스트의 구성방법

- 전역공간(자동으로 생성)
- eval()함수(악마로 취급)
- ✨ 함수 (가장 흔한 실행 컨텍스트 구성방법)
- `ES6`에서는 블록{}에 의해서도 새로운 실행 컨텍스트 생성

## 실행 컨텍스트와 콜스택

```js
// ---------------(1)
var a = 1;
function outer() {
  function inner() {
    console.log(a); //undefined
    var a = 3;
  }
  inner(); // ---------------(2) inner 함수 컨텍스트
  console.log(a); // 1
}
outer(); // ---------------(3) outer 함수 컨텍스트
console.log(a); // 1
```

자바스크립트 코드를 실행하는 순간

- 1️⃣ (1) 전역 컨텍스트가 콜 스택에 담김
- 2️⃣ 콜스택에는 전역 컨텍스트 외에 다른 것이 없으므로 전역 컨텍스트와 관련된 코드들을 순차로 진행
- 3️⃣ (3) outer 함수를 호출하면 자바스크립트 엔진은 outer에 대한 환경정보 수집 -> outer 실행 컨텍스트를 생성한 후 콜스택에 담음
- 4️⃣ 콜스택의 맨 위에 outer 실행 컨텍스트가 놓은 상태로, 전역 컨텍스트와 관련된 코드의 실행을 일시중단
- 5️⃣ outer 함수 내부의 코드들을 순차로 실행
- 6️⃣ (2) inner 함수의 실행 컨텍스트가 콜 스택의 가장 위에 담기면 outer 컨텍스트와 관련된 코드의 실행 중단
- 7️⃣ inner 함수 내부의 코드를 순서대로 진행

  ![](https://images.velog.io/images/hyehye/post/cf938d94-948e-4a93-a968-468854249b80/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-21%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.55.57.png)
  👉🏻 자바스크립트 엔진은 해당 컨텍스트에 관련된 코드들을 실행하는 데 피룡한 환경정보들을 수집해서 실행 컨텍스트 객체에 저장

## 실행 컨텍스트의 수집 정보

- `VariableEnvironment` : 현재 컨텍스트 내의 식별자들에 대한 정보 + 외부환경 정보(선언 시점의 LexicalEnvironment의 스냅샷으로, 변경사항 반영 X)
- `LexicalEnvironment` : 처음에는 VariableEnvironment와 같지만 변경 사항이 실시간으로 반영
- `ThisBinding` : this 식별자가 바라봐야 할 대상 객체

### VariableEnvironment

- LexicalEnvironment와 같지만 최초 실행 시의 스냅샷 유지
- 실행 컨텍스트 생성 시, VariableEnvironment에 정보를 먼저 담은 다음, 이를 그대로 복사해 LexicalEnvironment 생성, 이후 LexicalEnvironment 주로 활용
- environmentRecord와 outer-EnvironmentReference로 구성

### LexicalEnvironment

- '현재 컨텍스트의 내부에는 a,b,c와 같은 식별자들이 있고, 그 외부 정보는 D를 참조하도록 구성돼있다'라는, 컨텍스트를 구성하는 환경 저보들을 사전에서 접하는 느낌으로 모아놓은 것

### environmentRecord와 호이스팅

#### `environmentRecord`

- 현재 컨텍스트와 관련된 코드의 식별자 정보들이 저장
  - 컨텍스트를 구성하는 함수에 지정된 매개변수 식별자
  - 선언된 함수가 잇을 경우, 그 함수 자체
  - var로 선언된 변수의 식별자
- 컨텍스트 내부 전체를 처음부터 끝까지 쭉 훑어나가며 순서대로 수집
- 전역 실행 컨텍스트
  - 변수 객체를 생성하는 대신 자바스크립트 구동 환경이 별도로 제공하는 객체
  - 전역 객체에는 브라우저의 window, Node.js의 global 객체 등
  - 자바스크트립트 내장 객체(native object) ❌ / 호스트 객체(host object)로 분류 ⭕️

#### `호이스팅(hoistiong)`

- hoistiong : '끌어올리다'의 hoist에 ing를 붙여 만든 동명사 -> 식별자들을 최상단으로 끌어 올려 놓자
- 변수 정보를 수입하는 과정을 더욱 이해하기 쉬운 방법으로 대체한 가상의 개념
- 자바스크립트 엔진이 실제로 끌어올리지는 않지만 편의상 끌어올린 것으로 간주

🚀 매개변수와 변수에 대한 호이스팅(원본)

```js
function a(x) {
  // 수집 대상 1(매개변수)
  console.log(x); // (1)
  var x; // 수집 대상 2(변수 선언)
  console.log(x); // (2)
  var x = 2; // 수집 대상 3(변수 선언)
  console.log(x); //(3)
}
a(1);
```

- 호이스팅 개념을 모를 시, 예상 값
  - (1) : 함수 호출 시 전달한 1 출력
  - (2) : 선언된 변수 x에 할당된 값이 없으므로 undefined 출력
  - (3) : 변수 x에 할당된 2 출력
- 결과
  ![](https://images.velog.io/images/hyehye/post/addf8c6f-5c3d-4955-b968-c544be7067f1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-21%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.40.32.png)

🚀 매개변수와 변수에 대한 호이스팅 - 매개변수를 변수 선언/할당과 같다고 간주하여 변환한 상태

```js
function a() {
  var x = 1; // 수집 대상 1(매개변수 선언)
  console.log(x); // (1)
  var x; // 수집 대상 2(변수 선언)
  console.log(x); // (2)
  var x = 2; // 수집 대상 3(변수 선언)
  console.log(x); // (3)
}
a();
```

- 결과
  ![](https://images.velog.io/images/hyehye/post/1ef7b5b9-c8a8-4bf0-9e64-87e348301293/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-21%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.44.44.png)

🚀 매개변수와 변수에 대한 호이스팅 - 호이스팅

```js
function a() {
  var x; // 수집 대상 1의 변수 선언 부분
  var x; // 수집 대상 2의 변수 선언 부분
  var x; // 수집 대상 3의 변수 선언 부분

  x = 1; // 수집 대상 1의 할당 부분
  console.log(x); // (1)
  console.log(x); // (2)
  x = 2; // 수집 대상 3의 할당 부분
  console.log(x); // (3)
}
a(1);
```

- 결과
  ![](https://images.velog.io/images/hyehye/post/4d12cb5b-1fc2-4d7d-a087-5df895bd4e53/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-21%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.12.55.png)

🚀 함수 선언의 호이스팅 - 원본

```js
function a() {
  console.log(b); // (1)
  var b = "bbb"; // 수집 대상1 (변수 선언)
  console.log(b); // (2)
  function b() {} // 수집 대상2 (함수 선언)
  console.log(b); // (3)
}
a();
```

🚀 함수 선언의 호이스팅 - 호이스팅

```js
function a() {
  var b; // 수집 대상 1. 변수는 선언부만 끌어올린다.
  function b() {} // 수집 대상 2. 함수 선언은 전체를 끌어올린다.

  console.log(b); // (1)
  b = "bbb"; // 변수 할당부는 원래 자리에 남겨둔다.
  console.log(b); // (2)
  console.log(b); // (3)
}
a();
```

🚀 함수 선언의 호이스팅 - 함수 선언문을 함수 표현식으로 바꾼 코드

```js
function a() {
  var b;
  var b = function b() {}; // 바뀐 부분

  console.log(b); // (1)
  b = "bbb";
  console.log(b); // (2)
  console.log(b); // (3)
}
a();
```

- 결과
  ![](https://images.velog.io/images/hyehye/post/ecc03902-55b2-45d4-8f9f-79cd685566ff/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-21%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.38.01.png)

#### 함수 선언문과 함수 표현식

- 함수 선언문 : function 정의부만 존재하고 별도의 할당 명령이 없는 것.전체를 호이스팅 함.
  - 반드시 함수명이 정의돼 있어야 함
- 함수 표현식 : 정의한 function을 별도의 변수에 할당 하는 것

  - 기명 함수 표현식 : 함수명을 정의한 함수 표현식
  - 익명 함수 표현식 : 정의하지 않은 것(일반)

- 함수를 정의하는 세 가지 방식

```js
function a() {
  /* ... */
} // 함수 선언문. 함수명 a가 곧 변수명
a(); // 실행 OK

var b = function () {
  /* ... */
}; // (익명) 함수 표현식. 변수명 b가 곧 함수명.
b(); // 실행 OK

var c = function d() {
  /* ... */
}; // 기명 함수 표현식. 변수명은 c. 함수명은 d.
c(); // 실행 OK
d(); // 에러
```

#### 함수 선언문과 함수 표현식의 실질적인 차이

```js
//원본코드
console.log(sum(1, 2));
console.log(multiply(3, 4));

function sum(a, b) {
  // 함수 선언문 sum
  return a + b;
}

var multiply = function (a, b) {
  // 함수 표현식 multiply
  return a * b;
};
```

![](https://images.velog.io/images/hyehye/post/3bc1f750-036f-44ba-9fa9-8807e28f6fbd/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-21%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.37.07.png)

```js
//호이스팅
var sum = function sum(a, b) {
  //함수선언문 -> 함수 표현식으로 변환
  return a + b;
};
var multiply; // 변수는 선언부만 끌어올림
console.log(sum(1, 2));
console.log(multiply(3, 4));

multiply = function (a, b) {
  // 변수의 할당부는 원래 자리에 남김
  return a * b;
};
```

![](https://images.velog.io/images/hyehye/post/40b4eb7e-4063-46f6-9ff0-0ea2f6acb32a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-21%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.38.52.png)
🔥 함수 선언문은 함수선언, 초기화, 할당을 한번에 진행
🔥 함수 표현식은 함수 호이스팅이 아닌 변수 호이스팅을 진행하여 변수 생성 및 초기화와 할당이 분리되어 진행

> 💡 함수 선언문보다 상대적으로 함수 표현식이 안전하다.

### 스코프, 스코프 체인, outerEnvironmentReference

#### 스코프(Scope)

- 식별자에 대한 유효범위
- `함수스코프` : ES5에서는 함수에 의해서만 스코프 생성 -> var
- `블록스코프` : ES6에서는 블록에 의해서도 스코프 경계 발생 -> let, const, class, strict mode

#### 스코프 체인(Scope Chain)

- '식별자의 유효범위'를 안에서부터 바깥으로 차례로 검색해나가는 것
- 이를 가능케 하는 것이 바로 LexicalEnvironment의 두 번째 수집 자료인 outerEnvironmentReference

#### 변수 은닉화(variable shadowing)

- 상위 스코프에 선언되어 있지만, 현재 스코프에서 이미 선언된 경우네는 값이 할당되어 있지 않다고 하더라고 현재 스코프의 변수를 우선으로 한다는 규칙

#### 전역변수와 지역변수

- 전역변수(global variable) : 전역 공간에서 선언한 변수.
- 지역변수(local variable) : 함수 내부에서 선언한 변수.

> 참고 : 코어 자바스크립트(Core JavaScript), 정재남
