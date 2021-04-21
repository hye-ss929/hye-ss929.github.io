---
layout: post
title: Javascript - async & await
date: 2021-01-07
tags: [JavaScript]
---

## async & await

- async 와 await는 Promise를 간결/간편하고 동기적으로 실행되는것 처럼 보이게 만들어주는 API
- async 와 await는 새로운 것이 추가 된게 아니라, 기존에 존재하는 Promise 위에 조금 더 간편한 API를 제공함 (syntactic sugar)

### 1. async

- async를 사용하면 함수의 코드 블록이 자동으로 Promise로 변환이 되어짐

```jsx
async function fetchUser() {
  return "hello";
}

fetchUser().then(console.log); //함수로 바로 호출(받아오는 값이 같으므로 생략가능)
const user = fetchUser(); //변수에 할당하여 호출
user.then(console.log);
console.log(user);
```

### 2. await

- await는 async 함수 내부에만 사용 가능하다.
- error처리 : try / catch 사용

```jsx
function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(1000);
  return "🍎";
}

async function getBanana() {
  await delay(1000);
  return "🍌";
}

async function pickFruits() {
  const apple = await getApple();
  const banana = await getBanana();
  return `${apple} + ${banana}`;
}

pickFruits().then(console.log);
```

async와 await를 이용해서 동기적으로 코드를 작성하듯이, 원래 자연스럽게 코드를 작성하는 것처럼 리턴값도 자연스러우니 매우 간편하다.

### 3. await 병렬처리 - Promise APIs 사용

**<Promise.all>**

- Array 와 같이 순회 가능한(iterable) 객체에 포함된 모든 값을 담은 배열을 인자로 받고 여러 Promise 의 결과를 집계할 때 유용하게 사용

```jsx
function pickFruits() {
  return Promise.all([getApple(), getBanana()]).then((fruits) =>
    fruits.join(" + ")
  );
}

pickFruits().then(console.log);
```

![](https://images.velog.io/images/hyehye/post/323ab2d7-c46e-4203-bc7d-15702bb6f872/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.44.16.png)
getApple의 Promise와 getBanana의 Promise의 배열을 전달받아 받아진 배열을 전달받아 문자열로 변환해주었다.

**<Promise.race>**

- 가장 먼저 처리되는 Promise의 결과(혹은 에러)를 반환

```jsx
unction delay(ms) {
    return new Promise((resolve => setTimeout(resolve, ms)));
}

async function getApple() {
    await delay(2000);
    return '🍎';
}

async function getBanana() {
    await delay(1000);
    return '🍌';
}

function pickOnlyOne() {
    return Promise.race([getApple(), getBanana()]);
}

pickOnlyOne().then(console.log);
```

![](https://images.velog.io/images/hyehye/post/1a371f7f-5caa-49cf-a09a-aec29fad5e6a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.53.58.png)

🍌가 1초만에 전달되었기때문에 🍌만 출력되는 것을 볼 수 있다.

> 출처 : 드림코딩 by 엘리 https://youtu.be/aoQSOZfz3vQ
