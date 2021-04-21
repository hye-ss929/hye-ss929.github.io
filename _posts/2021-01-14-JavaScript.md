---
layout: post
title: JavaScript - arguments 객체
date: 2021-01-14
tags: [JavaScript]
---

## arguments

자바스크립트의 모든 함수는 내부에 arguments라는 변수를 가지고 있으며, 이 변수는 매개변수의 배열이다.

arguments는 함수를 호출할 때 넘긴 인자들이 배열 형태로 저장된 객체를 의미한다. 그래서 이 객체는 실제 배열이 아니고 "유사 배열 객체" 이다.

#### arguments 객체의 구성

- 함수를 호출할 때 넘겨진 인자(배열 형태)
- length 프로퍼티 : 호출할 때 넘겨진 인자의 개수
- callee 프로퍼티 : 현재 실행 중인 함수의 참조값

👉🏻 arguments 객체는 매개변수가 정확하게 정해지지 않은 함수를 구현하거나, 전달된 인자의 개수에 따라 서로 다르게 처리를 해줘야 하는 함수일 때 유용하게 사용 가능

length 프로퍼티는 배열과 유사하게 동작하지만 유사 배열 객체이므로 배열 메서드는 사용할 수 없다.

```jsx
//예시
function meetAt(year, month, date) {
  let length = arguments.length;

  if (length === 1) {
    return year + "년";
  } else if (length === 2) {
    return year + "년 " + month + "월";
  } else if (length === 3) {
    return year + "/" + month + "/" + date;
  }
}
```
