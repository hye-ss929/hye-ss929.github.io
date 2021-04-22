---
layout: post
title: JavaScript - this(2)
date: 2021-04-21 15:50 +0800
tags: [JavaScript]
excerpt: JavaScript - this(2)
---

# 자바스크립트 - this(2)

## 명시적으로 this를 바인딩 하는 방법

### call 메서드

```js
Function.prototype.call(thisArg[,arg1[,arg2,...]]])
```

- 메서드의 호출 주체인 함수를 즉시 실행하도록 하는 명령
- 첫 번째 인자를 this로 바인딩하고, 이후의 인자들을 호출할 함수의 매개변수로 함
- call 메서드를 이용하면 임의의 객체를 this로 지정 가능
  ![](https://images.velog.io/images/hyehye/post/c9a5f9ba-099f-4fd2-a90a-1cd502bef9a1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.02.47.png)
  ![](https://images.velog.io/images/hyehye/post/e3a6772f-79a3-4902-a9b7-f260806d9885/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.04.54.png)

### apply 메서드

```js
Function.prototype.aplly(thisArg[,argsArray])
```

- call 메서드와 기능적으로 완전히 동일
- 두 번째 인자를 배열로 받아 그 배열의 요소들을 호출할 함수의 매개변수로 지정
  ![](https://images.velog.io/images/hyehye/post/945f3f3f-21d0-4233-bbb2-55ea55083f92/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.08.08.png)

### call / apply 메서드의 활용

#### 유사배열객체에 배열 메서드를 적용

![](https://images.velog.io/images/hyehye/post/676d95fa-4a55-4045-b0a6-598963e6b35f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.11.13.png)

- 객체에는 배열 메서드 직접 적용 ❌
- 단, **키가 0 또는 양의 정수인 프로터피가 존재**하고 **length 프로퍼티의 값이 0 또는 양의 정수**인 객체
  - 배열의 구조와 유사한 객체의 경우(유사배열객체) call 또는 apply 메서드 이용해 배열 메서드 차용 가능
- `push`를 객체 obj에 적용해 프로퍼티 3에 'd' 추가
- `call` 메서드를 이용해 원본인 유사배열 객체의 얕은 복사 수행
- `slice` 메서드를 적용해 객체를 배열로 전환
  - 배열메서드이기 때문에 복사본은 배열로 반환

![](https://images.velog.io/images/hyehye/post/3d14b810-6b50-42fb-8110-97e1aa3bccad/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.18.55.png)

- 문자열의 경우 length 프로퍼티가 읽기 전용이기 때문에 원본 문자열에 변경을 가하는 메서드(push,pop,shift,unshift,splice 등)에는 error를 던짐

![](https://images.velog.io/images/hyehye/post/e2e079a3-b02d-4958-8111-1c62155f65e7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.22.54.png)

- concat처럼 대상이 반드시 배열이어야 하는 경우에는 에러는 나지 않지만, 제대로 된 결과 ❌

![](https://images.velog.io/images/hyehye/post/5a8f4e11-a838-4a19-bfa2-d9a0b42c36ba/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.25.13.png)

- ES6에서는 유사배열객체 또는 순회 가능한 모든 종류의 데이터 타입을 배열로 전환하는 Array.from 메서드 도입

#### 생성자 내부에서 다른 생성자를 호출

- 생성자 내부에 다른 생성자와 공통된 내용이 있을 경우
  - call or apply를 이용해 다른 생성사를 호출하면 간단하게 반복을 줄일 수 있음

![](https://images.velog.io/images/hyehye/post/d6a4fb47-51d9-430f-a2c2-8f52811340e2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.30.22.png)

#### 여러 인수를 묶어 하나의 배열로 전달하고 싶을 때 - apply 활용

- 여러 개의 인수를 받은 메서드에게 하나의 배열로 인수들을 전달하고 싶을 때 활용

![](https://images.velog.io/images/hyehye/post/18816a9c-995c-4d32-af29-b5237c0e5a7e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.32.39.png)

- ES6에서는 spread operator를 이용하면 apply보다 더욱 간편하게 작성 가능

![](https://images.velog.io/images/hyehye/post/c879d5ac-6d36-4904-a33b-c0700d88b013/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.34.49.png)

### bind 메서드

```js
Function.prototype.bind(thisArg[, arg1[,arg2[, ...]]])
```

- ES5에 추가된 기능
- call과 비슷하지만 즉시 호출하지 않고, 넘겨 받은 this 및 인수들을 바탕으로 새로운 함수를 반환하기만 하는 메서드
- 함수에 this를 미리 적용하는 것과 부분 적용 함수를 구현하는 두 가지 목적을 지님

![](https://images.velog.io/images/hyehye/post/248d25db-9a27-4e8f-8844-f0513638cb3f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.39.38.png)

#### name 프로퍼티

- bind 메서드를 적용해서 새로 만든 함수는 한 가지 독착한 성질이 있음
  - name 프로퍼티에 동사 bind의 수동태인 'bound'라는 접두어가 붙는다는 점
- 어떤 함수의 name 프로퍼티가 'bound xxx'라면 이는 곧 함수명이 xxx인 원본 함수에 bind 메서드가 적용한 새로운 함수라는 의미
- 기존의 call or apply보다 코드 추적이 수월함

![](https://images.velog.io/images/hyehye/post/f6163dc6-cf5f-437d-93b7-2e8fc0f3af05/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.44.11.png)

#### 상위 컨텍스트의 this를 내부함수나 콜백 함수에 전달하기

- call or apply or bind 메서드를 이용하여 메서드의 내부함수에서 메서드의 this를 그대로 바라보게 하기 가능
  ![](https://images.velog.io/images/hyehye/post/80cc8e99-db34-464a-af39-9759f75ffa1a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.57.47.png)

- 기본적으로 콜백 함수 내에서의 this에 관여하는 함수 또는 메서드에 대해서도 bind 메서드를 이용하면 this값을 사용자의 입맛에 맞게 수정 가능

![](https://images.velog.io/images/hyehye/post/53169c85-fc81-47e0-b6c3-2bd240d7645f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.00.54.png)

### 화살표 함수의 예외사항

- ES6에 새롭게 도입된 화살표 함수는 실행 컨텍스트 생성 시, this를 바인딩하는 과정 ❌
- 함수 내부에 this가 아예 없으며, 접근하고자 하면 스코프체인상 가장 가까운 this에 접근

![](https://images.velog.io/images/hyehye/post/98c8dc3b-0193-4c96-ab70-37bda9a1f4d3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.03.43.png)

- 별도의 변수로 this를 우회할 필요 ❌
- call/apply/bind 적용할 필요 ❌ , 더욱 간결하고 편리

### 별도의 인자로 this를 받는 경우(콜백 함수 내에서의 this)

- 콜백 함수를 인자로 받는 메서드 중 일부는 추가로 this로 지정할 객체(thisArg)를 인자로 지정할 수 있는 경우 ⭕️
- 이러한 메서드의 thisArg 값을 지정하면 콜백 함수 내부에서 this 값을 원하는 대로 변경 가능
- 배열 메서드에 많이 포진
- ES6에 새로 등장한 set,map 등의 메서드에도 일부 존재 / 그 중 대표적인 배열 메서드인 forEach

![](https://images.velog.io/images/hyehye/post/83ece802-e00f-4ed3-918f-96fa52eb2522/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.10.13.png)

#### 콜백함수와 함께 thisArg를 인자로 받는 메서드

```js
Array.prototype.forEach(callback[,thisArg])
Array.prototype.map(callback[,thisArg])
Array.prototype.filter(callback[,thisArg])
Array.prototype.some(callback[,thisArg])
Array.prototype.every(callback[,thisArg])
Array.prototype.find(callback[,thisArg])
Array.prototype.findIndex(callback[,thisArg])
Array.prototype.flatMap(callback[,thisArg])
Array.prototype.from(arrayLike[,(callback[,thisArg]])
set.prototype.forEach(callback[,thisArg])
Map.prototype.forEach(callback[,thisArg])
```

> 참고 : 코어 자바스크립트(Core JavaScript), 정재남
