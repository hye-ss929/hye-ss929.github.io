---
layout: post
title: Javascript - 콜백이해하기
date: 2021-01-05
tags: [JavaScript]
---

### 1. 동기와 비동기

#### 동기(Synchronous)

- 요청을 순차적으로 수행하며, 작업이 진행 중이면 다른 작업들은 대기한다.

#### 비동기(Asynchronous)

- 요청을 병렬적으로 수행하며, 어떤 작업이 종료되지 않았어도 기다리지 않고 다른 작업을 실행한다

```jsx
console.log("1");
setTimeout(() => console.log("2"), 1000);
console.log("3");
```

![](https://images.velog.io/images/hyehye/post/39fafffc-b4bb-49da-b553-ffd34284f99d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.36.09.png)
(1를 출력 후, setTimeout을 만나 브라우저에게 1초 뒤에 전달된 콜백을 실행해달라고 요청한 다음 3을 출력하고 브라우저에서는 1초 뒤 콜백함수를 실행하라 전달하면 2를 출력하게 된다.)

#### Synchronous callback

```jsx
function printImmediately(print) {
  print();
}
printImmediately(() => console.log("hello"));
```

#### Asynchronous callback

```jsx
function printWithDelay(print, timeout) {
  setTimeout(print, timeout);
}
printWithDelay(() => console.log("async callback"), 2000);
```

![](https://images.velog.io/images/hyehye/post/faf0490d-2fa5-4354-b24a-7975c9697a06/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.41.34.png)
위처럼 콘솔에서 확인할 수 있으며, 자바스크립트 엔진이 이해한 방법은 아래와 같다.

```jsx
//Synchronous callback
function printImmediately(print) {
  print();
}
// Asynchronous callback
function printWithDelay(print, timeout) {
  setTimeout(print, timeout);
}
//함수의 선언들이 전부 호이스팅되어 제일 위로 올라가게 된다.

console.log("1"); //동기
setTimeout(() => console.log("2"), 1000); //비동기
console.log("3"); //동기
printImmediately(() => console.log("hello")); //동기
printWithDelay(() => console.log("async callback"), 2000); //비동기
```

### 2. 콜백 지옥 체험

```jsx
class UserStorage {
  loginUser(id, password, onSuccess, onError) {
    setTimeout(() => {
      if (
        (id === "hyesung" && password === "qwerty") ||
        (id === "coder" && password === "zxcvb")
      ) {
        onSuccess(id);
      } else {
        onError(new Error("not found"));
      }
    }, 2000);
  }

  getRoles(user, onSuccess, onError) {
    setTimeout(() => {
      if (user === "hyesung") {
        onSuccess({ name: "hyesung", role: "admin" });
      } else {
        onError(new Error("no access"));
      }
    }, 1000);
  }
}
```

- id와 password 받아오기
- 로그인 실행
- 로그인이 성공적으로 된다면 id를 다시 받아와 role를 요청하기
- 사용자의 오브젝트 출력하기

```jsx
const userStorage = new UserStorage();
const id = prompt("enter your id");
const password = prompt("enter your password");
userStorage.loginUser(
  id,
  password,
  (user) => {
    userStorage.getRoles(
      user,
      (userWithRole) => {
        alert(
          `Hello ${userWithRole.name}, you have a ${userWithRole.role} role`
        );
      },
      (error) => {
        console.log(error);
      }
    );
  },
  (error) => {
    console.log(error);
  }
);
```

![](https://images.velog.io/images/hyehye/post/1fb29e2c-5d5f-45e7-8ca8-b844ec756775/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.03.29.png)
정상적으로 로그인이 되면, 네트워크에 요청을 해서 역할을 받아와 메세지가 뜨는 것을 확인할 수 있다.
만약 로그인에 실패했을 경우, 아무런 메세지가 뜨지않고 콘솔에 error가 나오는 것을 확인할 수 있다.
![](https://images.velog.io/images/hyehye/post/5e0cc059-5ddd-4553-a0b0-d851a535d57e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.05.57.png)

### 3. 콜백 지옥의 문제점

- 코드 가독성이 떨어진다.
- 비즈니스로직을 한 눈에 이해하는 것이 어렵다.
- 에러가 발생하거나 디버깅하기도 어렵다.
- 유지보수도 어렵다.

> 출처 : 드림코딩 by 엘리 https://youtu.be/s1vpVCrT8f4
