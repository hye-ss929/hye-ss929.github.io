---
layout: post
title: [Algorithm] 짝수와 홀수
date: 2021-04-30 12:54 +0800
tags: [Algorithm]
excerpt: 짝수와 홀수
---

#### 문제

정수 num이 짝수일 경우 "Even"을 반환하고 홀수인 경우 "Odd"를 반환하는 함수, solution을 완성해주세요.

#### 제한 조건

num은 int 범위의 정수입니다.
0은 짝수입니다.

#### 입출력 예

| num | return |
| :-: | :----: |
|  3  | "Odd"  |
|  4  | "Even" |

#### 문제풀이

```js
const solution = (num) => {
  return num % 2 === 0 ? "Even" : "Odd";
};
```

num이라는 매개변수를 받아서 2로 나누었을 때 나머지가 0이면 삼항연산자를 통해 true이면 Even을, false이면 Odd을 리턴하게 하였다.
