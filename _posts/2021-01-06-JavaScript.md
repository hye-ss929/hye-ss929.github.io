---
layout: post
title: Javascript - Promise
date: 2021-01-06
tags: [JavaScript]
---

## Promise

promise는 비동기 메서드에서 마치 동기 메서드처럼 값을 반환할 수 있습니다. 다만 최종 결과를 반환하지는 않고, 대신 프로미스를 반환해서 미래의 어떤 시점에 결과를 제공한다.

**상태 **

- pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
- fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- rejected(거부) : 비동기 처리가 실패하거나 오류가 발생한 상태

### 1. Producer (Promise 만들기)

- 새로운 Promise가 만들어질 때는 전달한 executor함수가 바로 실행이 된다.

```jsx
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(networt, read files)
  console.log("doing something...");
  setTimeout(() => {
    resolve("hello!");
  }, 2000);
});
```

![](https://images.velog.io/images/hyehye/post/71581b5e-cb86-4e36-a6f3-ef8dbaf1c85a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%201.37.17.png)
'doing something...'이후 2초 뒤에 hello!가 콘솔에 찍힌 것을 볼 수 있다.

### 2. Consumers : then, catch, finally (Promise 사용하기)

- then : promise 가 종료가 되면 resolve 에 들어간 값을 받을 수 있다.
- catch : reject 된 경우에는 then 으로 받을 경우, 에러가 발생하며 이 에러를 catch로 잡을 수 있다.
- finally : 성공과 실패와 관계없이 무조건 마지막에 호출되어진다.

```jsx
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(networt, read files)
  console.log("doing something...");
  setTimeout(() => {
    reject(new Error("no network"));
  }, 2000);
});
promise //
  .then((value) => {
    console.log(value);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => {
    console.log("finally");
  });
```

![](https://images.velog.io/images/hyehye/post/0bc67a85-4cf7-457c-8a44-d7114a225d22/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%201.49.34.png)

### 3. Promise chaining (Promise 연결하기)

```jsx
const fetchNuber = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000);
});
//1초 있다가 1를 전달

fetchNuber //
  .then((num) => num * 2) // 1*2 = 2
  .then((num) => num * 3) // 2*3 = 6
  .then((num) => {
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(num - 1), 1000); //6-1 = 5
    });
  })
  .then((num) => console.log(num));
```

then은 값을 바로 전달할수도 있고 Promise를 전달할 수도 있다.
2초의 시간 소요 뒤 5가 출력되는 것을 볼 수 있다.
![](https://images.velog.io/images/hyehye/post/4910cf8d-d317-46d7-b5e1-78bae5614b8c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%201.55.05.png)

### 4. 오류처리

```jsx
const getHen = () =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve("🐓"), 1000);
  });
const getEgg = (hen) =>
  new Promise((resolve, reject) => {
    setTimeout(() => reject(new Error(`${hen} => 🥚`)), 1000);
  });
const cook = (egg) =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${egg} => 🍳`), 1000);
  });
```

총 3가지의 프로미스를 리턴하는 함수로, 1초 있다가 🐓을 리턴, 🐓을 받아와서 🥚를 리턴, 🥚를 받아와서 🍳를 가정하였다.

```jsx
getHen()
  .then((hen) => getEgg(hen))
  .then((egg) => cook(egg))
  .then((cook) => console.log(cook));

// ⬇️ 한가지만 받아서 그대로 전달하는 경우에는 아래처럼 생략이 가능하여 짧게 표현할 수 있다.
getHen() //
  .then(getEgg)
  .then(cook)
  .then(console.log);
```

![](https://images.velog.io/images/hyehye/post/35f38a8f-7eef-4637-9cf2-d428e1eb54b4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.04.33.png)
에러를 잡지 않았기 때문에 에러메세지가 뜨는 것을 확인할 수 있다. 그리고 난 뒤 맨 뒤에 catch를 통해 에러를 잡아주게 되면 에러가 발생했지만 에러가 맨 아래로 전달되면서 catch가 잡힌 것을 볼 수 있다.

```jsx
getHen() //
  .then(getEgg)
  .then(cook)
  .then(console.log)
  .catch(console.log);
```

![](https://images.velog.io/images/hyehye/post/86548489-d013-49f5-9f25-8babdcea0065/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.07.56.png)

```jsx
getHen() //
  .then(getEgg)
  .catch((error) => {
    return "🥖";
  })
  .then(cook)
  .then(console.log)
  .catch(console.log);
```

계란을 받아올 때 문제가 생긴다면, 다른 걸로 대체해서 Promise 체인에 문제가 발생하지 않도록 처리를 할 수 있다.
![](https://images.velog.io/images/hyehye/post/93f68035-34e1-470d-962c-096f0cfbdf8a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.11.13.png)

### ✨ 콜백지옥 -> Promise 이용하기

지난 시간에 작성한 콜백지옥을 Promise를 이용하여 깔끔하게 코드처리 할 수 있다.

```jsx
class UserStorage {
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (
          (id === "hyesung" && password === "qwerty") ||
          (id === "coder" && password === "zxcvb")
        ) {
          resolve(id);
        } else {
          reject(new Error("not found"));
        }
      }, 2000);
    });
  }

  getRoles(user) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (user === "hyesung") {
          resolve({ name: "hyesung", role: "admin" });
        } else {
          reject(new Error("no access"));
        }
      }, 1000);
    });
  }
}

const userStorage = new UserStorage();
const id = prompt("enter your id");
const password = prompt("enter your password");
userStorage
  .loginUser(id, password)
  .then((user) => userStorage.getRoles(user))
  .then((user) => alert(`Hello ${user.name}, you have a ${user.role} role`))
  .catch(console.log);
```

> 출처 : 드림코딩 by 엘리 https://youtu.be/JB_yU6Oe2eE
