---
layout: post
title: [Algorithm] 평균구하기
date: 2021-04-29 12:54 +0800
tags: [Algorithm]
excerpt: 평균구하기
---

### 문제

정수를 담고 있는 배열 arr의 평균값을 return하는 함수, solution을 완성해보세요.

#### 제한사항

- arr은 길이 1 이상, 100 이하인 배열입니다.
- arr의 원소는 -10,000 이상 10,000 이하인 정수입니다.

#### 입출력 예

|    arr    | return |
| :-------: | :----: |
| [1,2,3,4] | [2.5]  |
|   [5,5]   |  [5]   |

---

### 문제풀이

```js
function solution(arr) {
  let answer = arr.reduce((prev, curr) => {
    return prev + curr;
  }, 0); // initialValue

  return answer / arr.length;
}
```

배열의 메소드인 `reduce()`를 활용하여 문제를 풀었다. `reduce()`는 배열의 각 요소를 하나씩 꺼내 사용자의 함수를 적용시킨 뒤, 그 값을 계속해서 누적시키는 함수이다.
curr은 배열에서 하나하나씩 전달이 되고, 리턴한 값이 다음에 호출될 때 prev로 연결되어 진다.
그리고 initialValue인 초기값을 0으로 설정해준다.

![](https://images.velog.io/images/hyehye/post/c6ae45b6-6b66-4cb6-9b1e-3d2726f48a2c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-29%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.12.10.png)

이후 총합이 나온 다음 배열의 길이만큼 나눠서 평균을 구할 수 있었다.
