---
layout: post
title: JavaScript - 프로토타입
date: 2021-04-22 23:53 +0800
tags: [JavaScript]
excerpt: JavaScript - 프로토타입
---

# 자바스크립트 - 프로토타입

## 프로토타입의 개념 이해

### constructor, prototype, instance

- 자바스크립트는 `프로토타입 기반 언어`
- 클래스 기반 언어에서는 `상속`을 사용, 프로토타입 기반 언어에서는 어떤 객체를 원형으로 삼고 이를 `복제(참조)`함으로써 상속과 비슷한 효과

[프로토타입 도식]
![](https://images.velog.io/images/hyehye/post/c511d7e4-dd24-4e0d-86ac-4c4caab80809/image.png)

```js
var instance = new Constructior();
```

![](https://images.velog.io/images/hyehye/post/1d2a5a66-f0bc-42a5-bee1-f5e9a7f22803/image.png)

- 어떤 생성자 함수(Constructor)를 new 연산자와 함께 호출하면
- Contructor에서 정의된 내용을 바탕으로 새로운 인스턴스(instance)생성
- 이때 instance에는 `__proto__`라는 프로퍼티가 자동으로 부여
- 이 프로퍼티는 Constructor의 prototype이라는 프로퍼티 참조

- `prototype` : 프로토타입 개념의 핵심. 객체

  - prototype 객체 내부에는 인스턴스가 사용할 메서드를 저장

- `__proto__` : 프로토타입 개념의 핵심. 객체
  - 인스턴스에서도 숨겨진 프로퍼티인 \_ _ proto _ \_를 통해 메서드들에게 접근

![](https://images.velog.io/images/hyehye/post/78d39ab6-5016-4e3f-9c2d-195b40178f93/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.24.04.png)

- Person의 인스턴스는 `__proto__`프로퍼티를 통해 getName을 호출할 수 있음
- instance의 `__proto__`가 Constructor의 prototype 프로퍼티를 참조 => 둘은 같은 객체를 바라봄

![](https://images.velog.io/images/hyehye/post/32f20047-56d4-4739-a4e6-e2a1c9f0ac3d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.27.04.png)

- 메서드 호출 결과 : undefined
- 어떤 변수를 실행해 undefined가 나왔다는 것은 이 변수가 '호출할 수 있는 함수'에 해당한다는 것을 의미
- 에러가 아닌 다른 값이 나왔으니 getName이 실제로 실행됐음을 알수있고, 이로부터 getName이 함수라는 것이 입증
- this에 바인딩된 대상이 잘못 지정된 것

[프로토타입 도식]
![](https://images.velog.io/images/hyehye/post/5bbd4e56-04e6-4645-bbac-0671208c9224/image.png)

- `__proto__`: 생략 가능한 프로퍼티
- new 연산자로 Constructor를 호출하면 instance 생성
- instance의 생략 가능한 `__proto__`는 Constructor의 prototype을 참고한다.
- **생성자 함수의 prototype에 어떤 메서드나 프로퍼티가 있다면 인스턴스에서도 마치 자신의 것처럼 해당 메서드나 프로터피에 접근 가능**

### constructor 프로퍼티

- 생성자 함수의 프로퍼티인 prototype 객체 내부에는 constuctor라는 프로퍼티 ⭕️
- 이 프로퍼티는 단어 그대로 원래의 생성자 함수(자기 자신)를 참조
- 인스턴스로부터 그 원형이 무엇인지를 알 수 있는 수단

![](https://images.velog.io/images/hyehye/post/3482f3e2-c2a1-45d7-84c0-08fb46297ef2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.14.57.png)

- 인스턴스의 `__proto__`가 생성자 함수의 prototype 프로퍼티를 참조하여 `__proto__`가 생략 가능
- 인스턴스에서 직접 constructor에 접근할 수 있는 수단 발생

#### 다양한 constructor 접근 방법

![](https://images.velog.io/images/hyehye/post/fda2b18c-0743-4352-b7c1-92d9db46007f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.20.24.png)
![](https://images.velog.io/images/hyehye/post/77c461fb-95d8-4029-b210-19080dee8432/image.png)

1. 모두 동일한 대상을 가리킴

```js
[Constructor][instance].__proto__.conmstructor[instance].constructor;
Object.getPrototypeOf([instance]).constructor[Constructor].prototype
  .constructor;
```

2. 모두 동일한 객체(prototype)에 접근 가능

```js
[Constructor].prototype[instance].__proto__[instance];
Object.getPrototypeOf([instance]);
```

## 프로토타입 체인

### 메서드 오버라이드

- prototype 객체를 참조하는 `__proto__`를 생략하면 인스턴스는 prototype에 정의된 프로퍼티나 메서드를 마치 자신의 것처럼 사용 가능
- 만약 인스턴스가 동일한 이름의 프로퍼티 또는 메서드를 갖고 있는 상황이라면?

![](https://images.velog.io/images/hyehye/post/6fc3a6da-93ec-47f5-99f7-ab372cfb9df5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.27.29.png)

- `iu.__proto__.getName`이 아닌 iu 객체에 있는 getName 메서드 호출
- 여기서 일어난 현상 - 메서드 오버라이드(메서드 위에 메서드를 덮어씌웠다는 표현)
- 원본을 제거하고 다른 대상으로 교체한 것이 아닌, 원본이 그대로 있는 상태에서 다른 대상을 그 위에 얹는 이미지
- 일반적으로 메서드가 오버라이드된 경우에는 자신으로부터 가장 가까운 메서드에만 접근할 수 있지만, 그다음으로 가까운 `__proto__`의 메서드도 우회적인 방법을 통해서이긴 하지만 접근 가능

### 프로토타입 체인

[객체의 내부구조]
![](https://images.velog.io/images/hyehye/post/6a74d30b-aa1f-4b47-80c8-a1ac58bfe2ab/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.32.14.png)

[배열의 내부구조]
![](https://images.velog.io/images/hyehye/post/943eea47-02a6-494e-9e01-f955ea467409/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.33.51.png)

[배열의 내부 도식]
![](https://images.velog.io/images/hyehye/post/c1033610-a754-4c10-a2fa-54a39db3f15a/image.png)

- `프로토타입 체인` : 어떤 데이터의 `__proto__`프로퍼티 내부에 다시 `__proto__` 프로퍼티가 연쇄적으로 이어진 것
- `프로토타입 체이닝` : 이 체인을 따라가며 검색하는 것

#### 메서드 오버라이드와 프로토타입 체이닝

![](https://images.velog.io/images/hyehye/post/3a52589f-104d-4bd6-9332-be2b4908de63/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.40.46.png)

- arr변수는 배열이므로 `arr.__proto__`는 Array.prototype을 참조
- Array.prototype은 객체이므로 `Array.prototype.__proto__`는 Object.prototype을 참조
- 이는 배열뿐만 아니라 자바스크립트 데이터는 모두 동일한 형태의 프로토타입 체인 구조

### 객체 전용 메서드의 예외사항

- 어떤 생성자 함수이든 prototype은 반드시 객체이기 때문에 Object.prototype이 언제나 프로토타입 체인의 최상단에 존재
- 객체에서만 사용할 메서드는 다른 여느 데이터 타입처럼 프로토타입 객체 안에서 정의 불가
- 객체에서만 사용할 메서드를 Object.prototype 내부에 정의한다면 다른 데이터 타입도 해당 메서드를 사용할 수 있기 때문

### 다중 프로토타입 체인

- 자바스크립트의 기본 내장 데이터 타입들은 모두 프로토타입 체인이 1단계(객체)이거나 2단계(나머지)로 끝나는 경우 다수
- 사용자가 새롭게 만드는 경우에는 그 이상도 얼마든지 가능
- 대각선의 `__proto__`를 연결해나가기만 하면 무한대로 체인 관계 가능
- 대각선의 `__proto__`를 연결하는 방법
  - `__proto__`가 가리키는 대상, 즉 생성자 함수의 prototype이 연결하고자 하는 상위 생성자 함수의 인스턴스를 바라보게끔 해주면 됌

> 참고 : 코어 자바스크립트(Core JavaScript), 정재남
