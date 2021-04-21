---
layout: post
title: Javascript - 연산 · 반복문
date: 2020-12-30
tags: [JavaScript]
---

### 1. String concatenation (문자열 연결)

```jsx
console.log("my" + "cat");
console.log("1" + "2");
console.log(`string literals:
1 + 2 = ${1 + 2}`);

console.log("hyesung's \nbook");
```

- string literals은 줄바꿈을 하거나 특수 기호도 그대로 출력한다.
- \n은 줄바꿈을 할 수 있다.

### 2. Numeric operators (숫자연산자)

```jsx
console.log(1 + 1); // +
console.log(1 - 1); // -
console.log(1 / 1); // /
console.log(1 * 1); // *
console.log(5 % 2); // 나머지
console.log(2 ** 3); // 제곱근
```

위처럼 연산자도 가능하다.

### 3. Increment and decrement operators (++,--)

```jsx
let counter = 2;

const preIncrement = ++counter;
console.log(`preIncrement: ${preIncrement}, counter: ${counter}`);
const preDecrement = --counter;
console.log(`preDecrement: ${preDecrement}, counter: ${counter}`);

const postIncrement = counter++;
console.log(`postIncrement: ${postIncrement}, counter: ${counter}`);
const postDecrement = counter--;
console.log(`postDecrement: ${postDecrement}, counter: ${counter}`);
```

- preIncrement / preDecrement : 증가 또는 감소 후 대입
- postIncrement / postDecrement : 대입 후 증가 또는 감소

### 4. Assignment operators (할당 연산자)

```jsx
let x = 3;
let y = 6;
x += y; // x = x + y
x -= y; // x = x - y
x *= y; // x = x * y
x /= y; // x = x / y
```

- 중복을 줄이기 위해 위처럼 코드 작성이 가능하다.

### 5. Comparison operators (비교연산자)

```jsx
console.log(10 < 6); // false
console.log(10 <= 6); // false
console.log(10 > 6); // true
console.log(10 >= 6); //true
```

```jsx
const value1 = True; //false에서 True로 변경
const value2 = 4 < 2; //false

console.log(`or: ${value1 || value2 || check()}`);

function check() {
  for (let i = 0; i < 10; i++) {
    //wasting time
    console.log("😭");
  }
  return true;
}
```

### 6. Logical operators: ||(or), &&(and), !(not) (논리연산자)

```jsx
const value1 = false; //false
const value2 = 4 < 2; //false

// ||(or) : 첫 값에 이미 True가 나오면 더이상 연산하지 않음 -> 연산이 오래걸리는 함수는 뒤에 배치
console.log(`or: ${value1 || value2 || check()}`);

// &&(and) : 첫 값에 이미 False가 나오면 더이상 연산하지 않음
console.log(`and: ${value1 && value2 && check()}`);
```

```jsx
function check() {
  for (let i = 0; i < 10; i++) {
    //wasting time
    console.log("😭");
  }
  return true;
}
```

check 함수를 만들어서 간단하게 시간을 쓰다가 True를 반환하게 하였다.

value1, value2 의 값이 false가 나오고, check의 값은 True가 나오므로 아래와 같이 나오는 것을 확인할 수 있다.
![](https://images.velog.io/images/hyehye/post/073d325b-637e-413b-99bb-a4c4df065181/1.png)

```jsx
const value1 = True; //false에서 True로 변경
const value2 = 4 < 2; //false

console.log(`or: ${value1 || value2 || check()}`);

function check() {
  for (let i = 0; i < 10; i++) {
    //wasting time
    console.log("😭");
  }
  return true;
}
```

value1의 값을 True로 변경하면 or 연산자는 첫 값에 이미 True가 나오면 더이상 연산하지 않기 때문에 그 뒤에 값이 false든 True든 상관없이 True값을 반환하기 때문에 😭이 나오지 않게 된다.
![](https://images.velog.io/images/hyehye/post/d3ed60e2-be1c-4594-8610-e65670b41de3/2.png)

```jsx
//!(not) : True값은 False로, False값은 True로 변환
console.log(!value1);
```

### 7. Equality (==,===)

```jsx
const stringFive = "5";
const numberFive = 5;
```

1. == : 타입상관안함

```jsx
console.log(stringFive == numberFive); //true
console.log(stringFive != numberFive); // false
```

2. === : 타입이 다르면 다른 타입으로 봄 (\*\* 코딩 시, 주로 사용할 것)

```jsx
console.log(stringFive === numberFive); //false
console.log(stringFive !== numberFive); //true
```

3. object : 각각 레퍼런스 형태로 저장

```jsx
const hyesung1 = { name: "hyesung" };
const hyesung2 = { name: "hyesung" };
const hyesung3 = hyesung1;
console.log(hyesung1 == hyesung2); //false
console.log(hyesung1 === hyesung2); //false
console.log(hyesung1 === hyesung3); //true 위에서 3을 1에 할당했기에 True
```

### 8. Conditional operators (조건연산자)

- if / else if

```jsx
const name = "hyesung";

if (name === "hyesung") {
  console.log("Welcome, Hyesung!"); // name이 hyesung일 경우, 출력
} else if (name === "coder") {
  console.log("You are amazing coder"); // name이 coder일 경우, 출력
} else {
  // 둘 다 아닐 경우 실행
  console.log("unkwnon");
}
```

### 9. Ternary operator (삼항 연산자)

- 조건 ? value1 : value2 → 조건식이 참이면 값1을, 거짓이면 값2를 출력한다.

```jsx
console.log(is_name === "hyesung" ? "yes" : "no");
```

### 10. Switch statement (switch 반목문)

- 여러 개의 if 조건문의 검사가 필요할 때 사용!

```jsx
const browser = "safari";

switch (browser) {
  case "IE":
    console.log("go away!");
    break;
  case "Chrome": // 출력문이 같을 때에는 케이스를 묶어서 표현 가능
  case "Firefox":
    console.log("love you!");
    break;
  default:
    console.log("same all!");
    break;
}
```

### 11. Loop(반복문)

1. while문 : 조건에 맞는 블럭을 실행하고 싶을 때 사용

```jsx
let i = 3;

while (i > 0) {
  console.log(`while: ${i}`);
  i--; //--는 감소
}
```

![](https://images.velog.io/images/hyehye/post/26ed8152-224b-4e6f-a141-32fbc5b3ccd4/3.png) 2) do while문 : 블럭을 먼저 실행하고 싶을 때 사용

```jsx
do {
  console.log(`do while: ${i}`);
  i--;
} while (i > 0); //실행하고 난 뒤 조건이 맞는지 안맞는지 확인
```

![](https://images.velog.io/images/hyehye/post/a1c89ddd-9a26-45fe-b61e-1f56fe616988/4.png) 3) for문 : for(begin; condition; step) - begin은 한번만 실행하고 condition과 step을 반복

```jsx
for (i = 3; i > 0; i--) {
  console.log(`for: ${i}`);
}

for (let i = 3; i > 0; i = i - 2) {
  console.log(`inline variable for: ${i}`);
}
```

![](https://images.velog.io/images/hyehye/post/2abb8f7d-f076-461c-b7a4-9d58c2d38c5d/5.png)
![](https://images.velog.io/images/hyehye/post/0aa98554-9ea5-48c5-b7ec-80cbf95ad054/6.png)

4. 중첩반복문

```jsx
for (let i = 0; i < 10; i++) {
  //10*10번 수행, O(n^2)로 추천하지 않음
  for (let j = 0; j < 10; j++) {
    console.log(`i: ${i}, j:${j}`);
  }
}
```

### 12. break, continue

- break : 루프를 완전히 끝내는 것
- continue : 스킵하고 다음으로 넘어가는 것

```jsx
// Q1. 1~10 사이의 짝수만 출력
// 예시1
for (let i = 0; i < 11; i++) {
  if (i % 2 !== 0) {
    continue;
  }
  console.log(`q1. ${i}`);
}
// 예시2
for (let i = 0; i < 11; i++) {
  if (i % 2 === 0) {
    console.log(`q1. ${i}`);
  }
}

// Q2. 0~10까지 출력하는데 8되면 종료
for (let i = 0; i < 11; i++) {
  if (i > 8) {
    break;
  }
  console.log(`q2. ${i}`);
}
```

> 출처 : 드림코딩 by 엘리 https://youtu.be/YBjufjBaxHo
