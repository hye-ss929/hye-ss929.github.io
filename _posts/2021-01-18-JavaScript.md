---
layout: post
title: JavaScript - Math 객체
date: 2021-01-18
tags: [JavaScript]
---

# Math

`Math`는 수학적인 상수와 함수를 위한 속성과 메서드를 가진 내장 객체이다.

Math 객체에 수학계산 메서드가 많이 있지만 그 중에서 자주 사용하는 것들만 정리해보려한다.

## 메서드

`Math.ceil` : 소수점 첫째 자리에서 올림

```jsx
Math.ceil(1.1); //1
Math.ceil(2.7); //3
```

`Math.floor` : 소수점 첫째 자리에서 내림

```jsx
Math.floor(2.49); //2
Math.floor(1.2); //1
```

`Math.round()` : 소수점 첫째 자리에서 반올림

```jsx
Math.round(3.1); //3
Math.round(4.6); //5
```

`Math.random()` : 0과 1 사이의 난수를 반환

```jsx
Math.random(); //0.804286431831789
```

## Math.random() - 랜덤함수

`Math.random()`함수는 0과 1 미만의 난수를 반환한다. 비록 0.0000000000000000에서 0.9999999999999999 사이의 값에서 랜덤수를 제공하지만, 이 랜덤함수를 이용해서 개발자가 원하는 범위의 랜덤수를 설정할 수 있다.

Math.random()이 아닌 `Math.floor`를 사용하면 더 균일한 랜덤 값을 생성할 수 있다. (Math.round를 사용하게 되면 0과 1이 나올 수 있는 확률이 절반으로 줄어들게 된다.)

```jsx
Math.floor(Math.random()); // 0
```

이렇게만 작성하게 되면 0만 나오게되니 범위를 지정해주고 사용하면 된다.

```jsx
Math.floor(Math.random() * 10); // 0 ~ 9의 랜덤 정수
Math.floor(Math.random() * 10) + 1; // 1 ~ 10의 랜덤 정수
```

### 두 값 사이의 난수 생성하기

: 함수의 반환값은 `min`보다 크거나 같으며, `max`보다 작다.

```jsx
function getRandomArbitrary(min, max) {
  return Math.random() * (max - min) + min;
}
```

### 두 값 사이의 정수 생성하기

: 반환값은 `min`(단, `min`이 정수가 아니면 보다 큰 최소의 정수)보다 크거나 같으며 `max`보다 작다.
: 최소값은 포함 / 최대값은 제외

```jsx
function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min)) + min;
```

### 최대값을 포함하는 두 값 사이의 정수 생성하기

: 최대값 - 최소값 포함

```jsx
function getRandomIntInclusive(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min; //최댓값도 포함, 최솟값도 포함
}
```
