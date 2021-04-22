---
layout: post
title: JavaScript - this(1)
date: 2021-04-21
tags: [JavaScript]
excerpt: JavaScript - this(1)
---

# JavaScript - this

## 상황에 따라 달라지는 this

- 자바스크립트에서 `this`는 기본적으로 실행 컨텍스트가 생성될 때 함께 결정
  => 즉, `this`는 **함수를 호출할 때 결정된다**
- 함수를 어떤 방식으로 호출하느냐에 따라 값이 달라진다.

### 전역 공간에서의 this

- 전역 공간에서 `this`는 "전역 객체"를 가리킴
- 전역 컨텍스트를 생성하는 주체 -> 전역객체이기 때문
- 전역 객체는 자바스크립트 런타임 환경에 따라 다른 이름과 정보
  - 브라우저 환경 : window
  - Node.js 환경 : global

![](https://images.velog.io/images/hyehye/post/1a2b4bd0-6c95-4215-ad3d-d16ce7121803/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.55.12.png)

#### 전역변수와 전역객체

```js
var a = 1;
console.log(a);
console.log(window.a);
console.log(this.a);
```

![](https://images.velog.io/images/hyehye/post/a038fa79-1548-46ed-9a2b-542455c12367/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.56.36.png)
전역공간에서 선언한 변수 a에 1을 할당했을 뿐인데 window.a와 this.a가 동일하게 1이 출력된다.
👉🏻 그 이유는, **자바스크립트의 모든 변수는 실은 특정 객체의 프로퍼티**로서 동작하기 때문

- 사용자가 var 연산자를 이용해 변수를 선언하더라도 실제 자바스크립트 엔진은 어떤 특정 객체의 프로퍼티로 인식(특정 객체란? 실행 컨텍스트의 LexicalEnvironment)
- 실행 컨텍스트는 변수를 수집하여 L.E의 프로퍼티로 저장
- 전역 컨텍스트의 경우, L.E는 전역객체 그대로 참조( = GlobalEnv가 전역 객체 참조 / 전역 컨텍스트의 L.E가 GlobalEnv 참조)

🔥 ** "전역변수를 선언하면 자바스크립트 엔진은 이를 전역객체의 프로퍼리로 할당한다"**

전역공간에서는 var로 변수를 선언하는 대신 `window의 프로퍼티에 직접 할당`하더라도 결과적으로는 `var로 선언한 것도 똑같이 동작할 것`이라는 예상 가능

```js
var a = 1;
window.b = 2;
console.log(a, window.a, this.a);
console.log(b, window.b, this.b);

window.a = 3;
b = 4;
console.log(a, window.a, this.a);
console.log(b, window.b, this.b);
```

![](https://images.velog.io/images/hyehye/post/38e73a8f-c26b-4fed-8af2-4bd6770405ed/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.08.19.png)

전역변수 선언과 전역객체의 프로퍼티 할당 사이에 전혀 다른 경우 ➡️ `삭제` 명령

- 전역 객체는 delete 명령이 불가능하고, 전역 객체의 프로퍼티는 delete 명령 동작
  - 이는 사용자가 의도치 않게 삭제하는 것을 방지하는 차원에서 마련한 나름의 방어 전략 해석

### 메서드로서 호출할 때 그 메서드 내부에서의 this

#### 함수 vs 메서드

- 함수
  - 그 자체로 독립적인 기능을 수행
  - 점(.)이나 대괄호같은 것 ❌

![](https://images.velog.io/images/hyehye/post/0cbea99f-fab2-47f6-a7a5-f9a6bdac5fe3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.22.22.png)

- 메서드
  - 자신을 호출한 대상 객체에 관한 동작 수행
  - 점(.)이나 대괄호같은 것 ⭕️

![](https://images.velog.io/images/hyehye/post/0a70e382-aeb3-4c67-8227-ac6f2eb0430d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.26.44.png)

#### 메서드 내부에서의 this

- 어떤 함수를 메서드로서 호출하는 경우, 호출 주체는 바로 `함수명(프로퍼티명) 앞의 객체`
- 점 표기법의 경우, `마지막 점 앞에 명시된 객체가 곧 this`

![](https://images.velog.io/images/hyehye/post/03a92b06-204e-4126-9610-c5f5d0be3f90/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.32.41.png)

### 함수로서 호출할 때 그 함수 내부에서의 this

#### 함수 내부에서의 this

- 어떤 함수를 함수로서 호출할 경우에는 this 지정 ❌
- 함수에서의 this는 전역 객체를 가리킨다.

#### 메서드의 내부함수에서의 this

![](https://images.velog.io/images/hyehye/post/2c4faa7a-5808-42db-add5-adfade10f0bf/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.41.28.png)
정답 ➡️ (1):obj1, (2):전역객체(window), (3):obj2

```js
1 var obj1 = {
2  outer:function() {
3    console.log(this);   //(1)
4    var innerFunc = function () {
5      console.log(this);  //(2) (3)
6    }
7    innerFunc();
8
9    var obj2 = {
10      innerMethod : innerFunc
11    };
12    obj2.innerMethod();
13  }
14 };
15 obj1.outer();
```

2️⃣ 번줄

- obj1.outer함수의 실행 컨텍스트 생성 및 호이스팅, 스코프 체인 정보수집, `this` 바인딩
- 함수를 호출할 때 함수명인 outer 앞에 점(.)이 있었으므로, `메서드`로서의 호출 ➡️ `마지막 점 앞의 객체인 obj1 바인딩`

4️⃣ 번줄

- innerFunc 함수의 실행 컨텍스트 생성 및 호이스팅, 스코프 체인 수집, this 바인딩 등 수행
- 함수를 호출할 때, 점(.) ❌
- 함수로서 호출한 것이므로, this가 지정 ❌ ➡️ 자동으로 스코프 체인상의 최상위 객체인 `전역객체(window) 바인딩`

9️⃣ 번줄

- obj2.innerMethod 함수의 실행 컨텍스트 생성
- 함수를 호출할 때 함수명인 innerMethod 앞에 점(.)이 있었으므로 `메서드`로서의 호출 ➡️ `마지막 점 앞의 객체인 obj2 바인딩`

🔥 오직 해당 함수를 호출하는 구문 앞에 점 또는 대괄호 표기가 있는지 없는지가 관건

#### 메서드의 내부 함수에서의 this를 우회하는 방법

✨ 변수를 활용하는 것

```js
var obj = {
  outer: function () {
    console.log(this); // (1) {outer: f}
    var innerFunc1 = function () {
      console.log(this); // (2) window{ ... }
    };
    innerFunc1();
    // 여기서 this를 변수에 할당
    var self = this;
    var innerFunc2 = function () {
      console.log(self); // (3) {outer: f}
    };
    innerFunc2();
  },
};
obj.outer();
```

#### this를 바인딩 하지 않는 함수

- 함수 내부에서 this가 전역객체를 바라보느나 문제를 보완하고자, this를 바인딩 하지않는 `화살표함수(arrow function)` 도입 (ES6)
- 화살표함수(arrow function)는 실행 컨텍스트를 생성할 때 this 바인딩 과정 자체가 빠지게 되어, `상위 스코프의 this를 그대로 활용 가능`

```js
var obj = {
  outer: function () {
    console.log(this);
    var innerFunc = () => {
      console.log(this);
    };
    innerFunc();
  },
};
obj.outer();
```

### 콜백 함수 호출 시 그 함수 내부에서의 this

- 함수 A의 제어권을 다른 함수(또는 메서드) B에게 넘겨주는 경우 함수 A를 `콜백함수`
- 함수 A는 함수 B의 내부 로직에 따라 실행
- this 역시 함수 B 내부 로직에서 정한 규칙에 따라 값 결정
- 제어권을 받은 함수에서 콜백 함수에 별도로 `this가 될 대상을 지정한 경우 그 대상을 참조`

### 생성자 함수 내부에서의 this

- `생성자 함수` : 어떤 공통된 성질을 지니느 객체들을 생성하는데 사용하는 함수
- 생성자 : 프로그래밍적으로 **구체적인 인스턴스를 만들기 위한** 일종의 틀
- 자바스크립트는 함수에 생성자로서의 역할을 함께 부여
  - new 명령어와 함께 함수를 호출하면 해당 함수가 생성자로서 동작
- 어떤 함수가 생성자 함수로서 호출된 경우 내부에서의 this는 `곧 새로 만들 국체적인 인스턴스 자신`

```js
var Cat = function (name, age) {
  this.bark = "야옹";
  this.name = name;
  this.age = age;
};
var choco = new Cat("초코", 7);
var nabi = new Cat("나비", 5);
console.log(choco, nabi);
```

![](https://images.velog.io/images/hyehye/post/91651d69-18fd-4a52-b0a2-e8a9249a261a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%203.17.37.png)

> 참고 : 코어 자바스크립트(Core JavaScript), 정재남
