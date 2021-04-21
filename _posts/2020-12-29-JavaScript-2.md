---
layout: post
title: JavaScript - 데이터타입
date: 2020-12-29
tags: [JavaScript]
---

### 1. 자바스크립트의 변수선언

#### \* Variable - 변경가능한, Read / Write

1. var

기존의 JavaScript(ES5)에서 변수 선언문으로, 아래와 같은 문제점이 있었다.

- 변수를 선언하기 전에 호출이 가능하다.(undefined)
- Function Scope(해당함수의 내부로 범위가 지정된 변수)를 갖는다.
- Block Scope({ }로 범위가 지정된 변수)가 없다.
- var hoisting(선언의 위치와 상관없이 항상 제일 위로 선언을 끌어 올려주는 것)

```jsx
console.log(age); //undefined
age = 4;
var age;
```

2. let

- ES6부터 변수 선언을 위해 만들어졌다.

```jsx
let name = "apple"; // let을 이용하여 a 변수를 선언하여 'apple' 값 할당
console.log(name);
name = "hello"; // a 변수에 'hello' 재할당
console.log(name);
```

![](https://images.velog.io/images/hyehye/post/58ed38a7-9c7a-422c-b203-abf595ebf7fd/1.png)

- block scope {}

{}(중괄호)를 이용하여 코드를 작성하게 되면 블럭 밖에서는 더이상 블럭 안에 있는 내용들을 볼 수 없게 된다.

```jsx
{
  let name = "apple";
  console.log(name);
  name = "hello";
}
console.log(name); // 값이 나오지 않음
```

- global scope

블록을 사용하지 않고 코드 내의 전 범위에서 사용이 가능하기 때문에 가능한 한 필요한 곳에만 사용하는 것이 좋다.

```jsx
let globalName = "global name";
console.log(globalName); // 중괄호 밖에서도 출력
{
  console.log(globalName); // 중괄호 안에서도 출력
}
```

#### _\* Contant - 변경불가능한, Read only_

1. const

- 보안성
- 스레드 안정성
- 코드를 변경했을 때의 실수를 방지

```
💡 변수 선언 시,
   Mutable 타입 let 사용 (변경가능한 타입)
   Immutable타입 const 사용 (변경이 불가한 타입)
```

```jsx
const daysInWeek = 7;
const maxNumber = 5;
```

#### \* Variable types 변경가능한 타입들

- 더이상 작은 단위로 나눠질 수 없는 타입(primitive, single item)

  : 숫자 / 문자 / 참과 거짓 / null / undefiedn / symbol

- object(싱글의 묶음) / box container
- function, first-class function

```jsx
const count = 17;
const size = 17.1;
console.log(`value: &{count}, type: ${typeof count}`); //type : number
console.log(`value: &{size}, type: ${typeof size}`); //type : number
```

1. 숫자(Number) - 특수한 숫자값 : infinity(무한대) / -infinity(-무한대) / NaN(Not a Number)

```jsx
const infinity = 1 / 0;
const negativeInfinity = -1 / 0;
const nAn = "not a numer" / 2;
console.log(infinity);
console.log(negativeInfinity);
console.log(nAn);
```

![](https://images.velog.io/images/hyehye/post/5a07b42a-4a06-49a4-ac18-ed5091293d5f/2.png)

2. 문자(String)

자바스크립트는 다른 언어와 달리 한 가지의 글자나 여러개의 글자 모두 string이다.

```jsx
const char = "c";
const tom = "tom";
const greeting = "hello" + tom;
console.log(`value: ${greeting}, type: ${typeof greeting}`); //type : string
const helloTom = `hi ${tom}!`;
console.log(`value: ${helloTom}, type: ${typeof helloTom}`); //type : string
```

```
💡 템플릿 문자열
   ``(backtick) 과 ${}를 사용하면 더욱 편리하게 문자열을 생성할 수 있다.
```

3. 참과 거짓(boolean)

- False : 0 / null / undefined / NaN / ' '
- True : any other value ( 다른 값)

```jsx
const canRead = true;
const test = 3 > 1; // fales
console.log(`value: ${canRead}, type:${typeof canRead}`);
console.log(`value: ${test}, type:${typeof test}`);
```

4. null (텅텅 비어있는 값)

```jsx
let nothing = null;
console.log(`value:${nothing}, type: ${typeof nothing}`); // type : object
```

5. undefined (선언은 해두었으나 값이 지정이 안 된 경우)

```jsx
let x;
console.log(`value: ${x}, type: ${typeof x}`); // type : undefined
```

6. symbol, create unique identifiers for objects (고유한 식별자가 필요하거나 동시다발적으로 일어나는 코드에서 우선순위를 주고 싶을 때)

```jsx
const symbol1 = Symbol("id");
const symbol2 = Symbol("id");
console.log(symbol1 === symbol2); // False

const symbol1 = Symbol.for("id");
const symbol2 = Symbol.for("id");
console.log(symbol1 === symbol2); // True
console.log(`value: ${symbol1.description}, type: ${typeof symbol1}`);
```

#### \* Dynamic typing - 동적 타이핑

```jsx
let text = "hello";
console.log(text.charAt(0)); // 인덱싱
console.log(`value: ${text}, type: ${typeof text}`); // type : string
text = 1;
console.log(`value: ${text}, type: ${typeof text}`); // type : number
text = "7" + 5;
console.log(`value: ${text}, type: ${typeof text}`); // type : string
text = "8" / "2";
console.log(`value: ${text}, type: ${typeof text}`); // type : number
```

```
💡 변수 설정에 따라 string 또는 number 로 중간에 바뀌기도 하니 주의할 것!
```

> 출처 : 드림코딩 by 엘리 https://youtu.be/OCCpGh4ujb8
