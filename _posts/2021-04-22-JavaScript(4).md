---
layout: post
title: JavaScript - 클로저
date: 2021-04-22 19:46 +0800
tags: [JavaScript]
excerpt: JavaScript - 클로저
---

# 자바스크립트 - 클로저

## 클로저의 의미 및 원리 이해

- `클로저(Closure)`: 여러 함수형 프로그래밍 언어에서 등장하는 보편적인 특성
- MDN에서는 클로저에 대해 **클로저는 함수와 그 함수가 선언될 당시의 lexical environment의 상호관계에 따른 현상"**이라 설명
- 여기서 Lexical Environment는 실행 컨텍스트의 구성 요소 중 하나인 `outerEnvironmentReference`에 해당
- **내부함수에서 외부 변수를 참조하는 경우**인 **combination**
  - 즉, 선언될 당시의 LexicalEnvironment와의 상호환계를 의미

#### 외부함수의 변수를 참조하는 내부 함수

```js
var outer = function () {
  var a = 1;
  var inner = function () {
    console.log(++a);
  };
  inner();
};
outer();
```

- outer 함수에서 변수a를 선언, outer의 내부함수인 inner 함수에서 a의 값을 1만큼 증가시킨 다음 출력
- inner 함수 내부에서는 a를 선언하지 않았기 때문에 environmentRecord에서 값을 찾지 못하므로 outerEnviromentRefernce에 지정된 상위 컨텍스트인 outer의 LexicalEnvironment에 접근해서 다시 a 찾음
- outer함수의 실행 컨텍스트가 종료되면 LexicalEnvironment에 저장된 식별자들(a, inner)에 대한 참조 삭제
- 각 주소에 저장돼 있던 값들은 자신을 참조하는 변수가 하나도 없게 되므로 가비지 컬렉터의 수집 대상

#### 외부함수의 변수를 참조하는 내부 함수(2)

```js
var outer = function () {
  var a = 1;
  var inner = function () {
    return ++a;
  };
  return inner();
};
var outer2 = outer();
console.log(outer2);
```

- inner 함수 내부에서 외부변수인 a 사용
- inner 함수를 실행한 결과를 리턴, 결과적으로 outer 함수의 실행 컨텍스트가 종료된 시점에는 a 변수를 참조하는 대상 ❌
- a, inner 변수의 값들은 언젠가 가비지 컬렉터에 의해 소멸

#### 외부 함수의 변수를 참조하는 내부 함수(3)

- outer의 실행 컨텍스트가 종료된 후에도 inner함수를 호출할 수 있게 만들기

```js
var outer = function () {
  var a = 1;
  var inner = function () {
    return ++a;
  };
  return inner;
};
var outer2 = outer();
console.log(outer2()); //2
console.log(outer2()); //3
```

1.

- inner 함수의 실행 결과가 아닌 inner 함수 자체를 반환
- outer 함수의 실행 컨텍스트가 종료될 때 outer2 변수는 outer의 실행 결과인 inner 함수를 참조
- outer2 를 호출하면 앞서 반환된 inner 함수 실행

2.

- inner 함수의 실행 컨텍스트의 environmentRecord에는 수집할 정보 ❌
- outer-EnvironmentReference에는 inner 함수가 선언된 위치의 L.E가 참조 복사
- inner 함수는 outer 함수 내부에서 선언, outer 함수의 L.E가 담길 것
- 스코프 체이닝에 따라 outer에서 선언한 변수a에 접근해서 1만큼 증가시킨 후 그 값이 2를 반환, inner 함수의 실행 컨텍스트 종료

3.

- inner 함수의 실행 시점에는 outer함수가 이미 실행 종료됐음에도 불구하고 변수a에 접근
  - 왜? 이는 가비지 컬렉터의 동작방식 때문
  - 가비지 컬렉터는 어떤 값을 참조하는 변수가 하나라도 있다면 그 값은 수집 대상 포함 ❌
- 외부함수인 outer의 실행이 종료되더라도 내부 함수인 inner함수의 실행 컨텍스크가 활성화되면 outerEnvironmentRefernce가 outer 함수의 L.E를 필요로 할 것이므로 수집 대상에서 제외
  - 그 덕에 inner 함수가 변수에 접근 가능

> 💡 **클로저**란, 어떤 함수 A에서 선언한 변수a를 참조하는 내부 함수 B를 외부로 전달할 경우 A의 실행 컨텍스트가 종료된 이후에도 변수 a가 사라지지 않는 현상

## 클로저와 메모리 관리

- 클로저는 객체지향과 함수형 모두를 아우르는 매우 중요한 개념
- 메모리 소모는 클로저의 본질적인 특성

### 메모리 관리 방법

- 클로저는 어떤 필요에 의해 의도적으로 함수의 지역변수를 메모리를 소모하도록 함으로써 발행 ➡️ 그 필요성이 사라진 시점에는 더는 메모리를 소모하지 않게 해주면 됨
- 즉, `참조카운터를 0`으로 하면 된다.
- 참조 카운터를 0으로 만드는 방법
  - 식별자에 참조형이 아닌 기본형 데이터(보통 null 이나 undefined)를 할당

#### (1) return에 의한 클로저의 메모리 해제

```js
var outer = (function () {
  var a = 1;
  var inner = function () {
    return ++a;
  };
  return inner;
})();
console.log(outer());
console.log(outer());
outer = null; //outer 식별자의 inner 함수 참조를 끊음
```

#### (2) setInterval에 의한 클로저의 메모리 해제

```js
(function () {
  var a = 0;
  var intervalId = null;
  var inner = function () {
    if (++a >= 10) {
      clearInterval(intervalId);
      inner = null; // inner 식별자의ㅣ 함수 참조를 끊음
    }
    console.log(a);
  };
  intervalId = setInterval(inner, 1000);
})();
```

#### (3) eventListener에 의한 클로저의 메모리 해제

```js
(function () {
  var count = 0;
  var button = document.createElement("button");
  button.innerText = "click";

  var clickHandler = function () {
    console.log(++count, "times clicked");
    if (count >= 10) {
      button.removeEventListener("click", clickHandler);
      clickHandler = null; //clickHandler 식별자의 함수 참조를 끊음
    }
  };
  button.addEventListener("click", clickHandler);
  document.body.appendChild(button);
})();
```

## 클로저 활용 사례

### 접근 권한 제어(정보 은닉)

- `정보 은닉` : 어떤 모듈의 내부 로직에 대해 외부로의ㅣ 노출을 최소하해서 모듈간의 결합도를 낮추고 유연성을 높이고자 하는 현대 프로그래밍 언어의 중요한 개념
- 접근 권한 : public, private, protected
  - public : 외부에서 접근 가능한 것
  - private : 내부에서만 사용하며 외부에 노출되지 않는 것

### 부분 적용 함수

- `부분 적용 함수` : n개의 인자를 받는 함수에 미리 m개의 인자만 넘겨 기억시켰다가, 나중에 (n -m)개의 인자를 넘기면 비로소 원래 함수의 실행 결과를 얻을 수 있게끔 하는 함수
- 디바운스 : 짧은 시간 동안 동일한 이벤트가 많이 발생할 경우 이를 전부 처리하지 않고 처음 또는 마지막에 발생한 이벤트에 대해 한번만 처리 하는 것(프론트 엔드 성능 최적화에 큰 도움을 주는 기능 중 하나)
  - scroll, wheel, mousemove,resize 등 적용

### 커링 함수

- `커링 함수`: 여러 개의 인자를 받는 함수를 하나의 인자만 받는 함수로 나눠서 순차적으로 호출될 수 있게 체인 형태로 구성한 것
- 한 번에 하나의 인자만 전달하는 것을 원칙
- 중간 과정 상의 함수를 실행한 결과는 그 다음 인자를 받기 위해 대기만 할 뿐, 마지막 인자가 전달되기 전까지는 원본 함수가 실행되지 않음
- 다만, 인자가 많아질수록 가독성이 떨어짐

> 참고 : 코어 자바스크립트(Core JavaScript), 정재남
