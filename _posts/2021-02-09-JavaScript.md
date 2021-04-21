---
layout: post
title: JavaScript - spread syntax
date: 2021-02-09
tags: [JavaScript]
excerpt: spread syntax
---

# spread syntax

배열이나 문자열과 같이 반복 가능한 문자를 0개 이상의 인수 (함수로 호출할 경우) 또는 요소 (배열 리터럴의 경우)로 확장하여, 0개 이상의 키-값의 쌍으로 객체로 확장시킬 수 있는 문법으로 '...'을 사용한다.

#### 1. Copy(복사)

기존에 하나하나씩 복사는 할 때는 배열의 map 또는 foreach를 이용할 수 있었으나, spread syntax를 이용하여 아래와 같이 간단하게 표현할 수 있다.

```js
// array copy
const arr = [1, 2, 3, 4, 5];
const arraycopy = [...arr]; //[1, 2, 3, 4, 5]
```

👉🏻 ...은 array에 들어있는 아이템 하나하나씩을 각각 낱개로 가져와서 복사해오는 것을 말한다.

```js
// obj copy
const obj = { key1: "🍏", key2: "🍎" };
const objcopy = { ...obj }; // {key1 : '🍏', key2 : '🍎'}
```

👉🏻 object를 가리키고 있는 변수는 실제로 object를 담고 있는 것이 아닌 object가 들어있는 메모리의 주소값을 가지고 있다. 그래서 동일한 object를 가리키고 있는 것이다.

```js
// obj copy
obj.key1 = "🍌";
const objcopy = { ...obj }; //{key1 : '🍌', key2 : '🍎'}
```

👉🏻 key1을 '🍌'로 변경하고 다시 출력한 뒤 확인을 해보면 값이 변경된 것을 볼 수 있다.

✨✨✨ spread 연산자는 object가 가리키고 있는 주소의 참조값만을 복사해오기때문에 원래의 object를 변경하게 되면 spread 해온 값에 영향을 주기에 유의해서 사용할 것!✨✨✨

#### 2. Concatenation (연결)

```js
// array
const animal1 = ["🐶", "🐱", "🐭"];
const animal2 = ["🐹", "🦊", "🐰"];
const animals = [...animal1, ...animal2]; // ['🐶', '🐱', '🐭','🐹', '🦊', '🐰']
```

```js
// obj
const weather1 = { sun: "☀️" };
const weather2 = { rain: "🌧" };
const weather = { ...weather1, ...weather2 }; //{sun : '☀️', rain : '🌧'}
```

```jsx
const flower1 = { rose: "🌷" };
const flower2 = { rose: "🌹" };
const flower = { ...flower1, ...flower2 }; //{rose : '🌹'}
```

👉🏻 만약 key가 동일한 object를 병합하게 되면 제일 뒤에 있는 내용이 앞에 있는 내용을 덮어씌우기 때문에 주의할 것!
