---
layout: post
title: Javascript - Function함수
date: 2020-12-31
tags: [JavaScript]
---

### Function

- 기본적인 빌딩블럭
- 서브프로그램이라 불리며, 여러번 재사용 가능
- 한 가지 일이나 값을 계산할 때 사용

#### 1. Functoin declaration (함수선언)

- function name(param1,param2){body... return;}
- 하나의 함수에는 한 가지 일만 (one function === one thing)
- naming: doSomething, command, verb
- JS에서 함수는 object

```jsx
function printHello() {
  //함수정의
  console.log("Hello");
}
printHello(); //함수호출
```

```jsx
function log(message) {
  // message를 parameter로 전달
  console.log(message);
}
log("Hello, hyesung!");
log(1234);
```

#### 2. Parameters (매개 변수)

- primitive parameters: passed by value (값으로 전달)
- object parameters: passed by reference (참조로 전달)

```jsx
function changeName(obj) {
  //obj의 위치가 전달
  obj.name = "coder";
}
const hyesung = { name: "hyesung" };
changeName(hyesung); // changeName(hyesung)를 전달하면 hyesung이 가르키고 있는 곳에 이름을 coder로 변경함
console.log(hyesung);
```

![](https://images.velog.io/images/hyehye/post/2e2e618c-92b4-48a4-ad3b-442061a65233/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-28%20%EC%98%A4%ED%9B%84%202.43.15.png)

#### 3. Default parameters (ES6에 추가)

```jsx
function showMessage(message, from = "unknown") {
  //조건문이 없어도 default값 지정가능
  console.log(`${message} by ${from}`);
}
showMessage("Nice meet you!");
```

![](https://images.velog.io/images/hyehye/post/83aeeddc-b228-45e7-a120-43d237e5b367/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-28%20%EC%98%A4%ED%9B%84%202.43.24.png)

#### 4. Rest parameters (ES6에 추가)

```jsx
function printAll(...args) {
  //배열형태
  for (let i = 0; i < args.length; i++) {
    console.log(args[i]);
  }
  // 또는
  for (const arg of args) {
    console.log(arg);
  }
  // 또는
  args.forEach((arg) => console.log(arg));
}
printAll("hi", "hyesung", "love"); //3개의 인자를 배열로 출력
```

![](https://images.velog.io/images/hyehye/post/d3eca32f-b030-4e6b-8046-1a22faf944c3/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-28%20%EC%98%A4%ED%9B%84%202.43.35.png)

#### 5. Local scope

밖에서는 안을 볼 수 없고, 안에서만 밖을 볼 수 있다.

```jsx
let globalMessage = "global"; //전역변수
function printMessage() {
  let message = "hello";
  console.log(message); //지역변수(블럭 내에서만 유효)
  console.log(globalMessage);
  function printAnother() {
    console.log(message);
    let childMessage = "hello";
  }
  //console.log(childMessage); //error
}
printMessage();
```

#### 6. Return a value

```jsx
function sum(a, b) {
  return a + b;
}
const result = sum(1, 2); //result에 3을 저장
console.log(`sum: ${sum(1, 2)}`);
```

#### 7. Early return, early exit (조기 리턴-조기 종료 / 실무에서 유용)

```jsx
// bad
function upgradeUser(user) {
  if (user.point > 10) {
    //long upgrade logic...
  }
}

// good ( 조건이 맞지 않을 때는 빠른 리턴으로 함수 종료)
function upgradeUser(user) {
  if (user.point <= 10) {
    return;
  }
  //long upgrade logic...
}
```

```
💡 First-class function
   함수는 변수처럼 할당되고 parameter로 전달되며 다른 함수에 의해 return될 수 있음
```

1. Function expression (함수표현)

- 함수의 정의, 선언 이전에는 함수는 호출될 수 있음(hoisted)

```jsx
const print = function () {
  //anonymous function(이름없는 함수)를 변수에 저장
  console.log("print");
};
print(); //print : print  변수를 함수처럼 호출
const printAgain = print; // 또 다른 변수에 재할당
printAgain();
const sumAgain = sum; //sum함수에 변수를 재할당
console.log(sumAgain(1, 3));
```

![](https://images.velog.io/images/hyehye/post/d623aae8-d8ff-47c3-99eb-6d2ae23098e2/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-28%20%EC%98%A4%ED%9B%84%202.43.44.png) 2. callback function

- 타 함수의 parameter로 이용되는 함수
- 특정 이벤트가 발생하면 수행될 함수

```jsx
function randomQuiz(answer, printYes, printNo) {
  //printYes, printNo =>callback 함수
  if (answer === "love you") {
    printYes();
  } else {
    printNo();
  }
}

// anonymous function
const printYes = function () {
  console.log("yes!");
};

//named function
//- 디버깅시 함수를 구분해야 할 때
//- 재귀함수 만들 떄 사용(무한적으로 순환 반복)
const printNo = function print() {
  console.log("no!");
};
randomQuiz("like you", printYes, printNo);
randomQuiz("love you", printYes, printNo);
```

![](https://images.velog.io/images/hyehye/post/1da7f4e1-79e6-4f7b-a7ec-3133574b6cbc/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-28%20%EC%98%A4%ED%9B%84%202.43.50.png)

### Arrow fuction

- 항상 anonymous function
- 함수를 간결하게 만들어 준다.

```jsx
// const simplePrint = function () {
//     console.log('simplePrint');
// };

const simplePrint = () => console.log("simplePrint!");
const add = (a, b) => a + b; //괄호 안 parameter, =>에 return값 표기
const simpleMultiply = (a, b) => {
  //복잡한 코드 사용 시, 블럭표기
  // 복잡한 코드표기
  return a * b;
};
```

### IIFE(Immediately Invoked Function Expression)

- 선언과 동시에 함수를 호출하는 방식
- 함수의 선언과 표현식을 괄호로 묶음
- 현업에서는 잘 사용하지 않음

```jsx
(function hello() {
  console.log("IIFE");
})();
```

> 출처 : 드림코딩 by 엘리 https://youtu.be/e_lU39U-5bQ
