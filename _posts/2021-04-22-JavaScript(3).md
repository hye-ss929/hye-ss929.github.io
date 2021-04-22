---
layout: post
title: JavaScript - 콜백함수
date: 2021-04-22 17:50 +0800
tags: [JavaScript]
excerpt: JavaScript - 콜백함수
---

# 자바스크립트 - 콜백함수

- 콜백 함수 : 다른 코드의 인자로 넘겨주는 함수
- `제어권`과 관련이 깊음
- 어떤 함수 X를 호출하면서 '특정 조건일 때 함수 Y를 실행해서 나에게 알려달라'는 요청을 함께 보냄
  - 이 요청을 받은 함수 X의 입장에서는 해당 조건이 갖춰졌는지 여부를 스스로 판단하고 Y를 직접 호출
    👉🏻 다른 코드(함수 또는 메서드)에게 인자로 넘겨줌으로써 그 제어권도 함께 위임한 함수

## 제어권

### 호출 시점

![](https://images.velog.io/images/hyehye/post/7fb4f31e-ec14-4c1b-a2ad-61b7599e1b3c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.29.09.png)

- timer 변수를 선언하고 여기에 setInterval 실행한 결과 할당
- setInterval을 호출할 때 두개의 매개변수 전달
  - 첫 번째, 익명함수
  - 300이라는 숫자

```js
//setInterval의 구조
var intervalID = scope.setInterval(func, delay[, param1, param2, ...]);
```

- 매개변수로는 func, delay값을 반드시 전달해야 하고, 세 번째 매개변수부서는 선택적
- setInterval를 실행하면 반복적으로 실행되는 내용 자체를 특정할 수 있는 고유한 ID값 반환
  - 변수에 담는 이유 : 반복 실행되는 중간에 종료(clearInterval)할 수 있게 하기 위해서

### 인자

![](https://images.velog.io/images/hyehye/post/df124cf1-b856-4e1e-86cf-f7e0b355ea18/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.36.42.png)

Array의 prototype에 담긴 map 메서드의 구조

```js
Array.prototype.map(callback[, thisArg])
callback:function(currentValue, index, array)
```

- 첫 번째 인자로 callback 함수를 받고, 생략 가능한 두 번째 인자로 콜백 함수 내부에서 this로 인식할 대상을 특정
- map 메서드는 메서드의 대상이 되는 배열의 모든 요소들을 처음부터 끝까지 하나씩 꺼내어 콜백 함수를 반복 호출 -> 콜백함수의 실행 결과들을 모아 새로운 배열로 만듬
- 콜백 함수의 첫 번째 인자에는 배열의 요소 중 현재값이,
- 두 번째 인자에는 현재값의 인덱스가,
- 세 번째 인자에는 map의 대상이 되는 배열 자체

### this

![](https://images.velog.io/images/hyehye/post/2d7f2ad6-cfe7-4829-b51c-80adf0f5dab2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.45.20.png)

- this에는 thisArg 값이 있을 경우에는 그 값을, 없을 경우에는 전역객체를 지정
- 첫 번째 인자엔느 메서드의 this가 배열을 가리킬 것이므로 배열의 i번째 요소 값
- 두 번째 인자에는 i 값
- 세 번째 인자에는 배열 자체를 지정해 호출

=> 제어권을 넘겨받을 코드에서 call/apply 메서드의 첫 번째 인자에 콜백 함수 내부에서의 this가 될 대상을 명시적으로 바인딩 하기 때문

## 콜백 함수는 함수다

- 콜백 함수는 어떤 객체의 메서드를 전달하더라도 그 메서드는 메서드가 아닌 함수로서 호출

```js
1 var obj = {
2  vals:[1,2,3],
3   logValues: function (v, i) {
4     console.log(this, v, i);
5   }
6 };
7 obj.logValues(1,2);
8 [4,5,6].forEach(obj.logValues);
```

![](https://images.velog.io/images/hyehye/post/38092dbd-bce2-4246-8558-02424c295590/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.53.47.png)

- 7️⃣ 번째 줄 : 메서드의 이름 앞에 점(.)이 있으니 메서드로서의 호출
  - this는 obj를 가리킴
- 8️⃣ 번째 줄 : 메서드를 forEach 함수의 콜백 함수로서 전달
  - obj.logValues가 가리키는 함수만 전달
  - forEach함수에 의해 콜백이 함수로서 호출되고, 별도로 this를 지정하는 인자를 지정하지 않았으므로 => 함수 내부에서의 this는 전역 객체

## 콜백 함수 내부의 this에 다른 값 바인딩 하기

```js
var obj1 = {
  name: "obj1",
  func: function () {
    var self = this;
    return function () {
      console.log(self.name);
    };
  },
};
///
var obj2 = {
  name: "obj2",
  func: obj1.func,
};
var callback2 = obj2.func();
setTimeout(callback2, 1500);

var obj3 = { name: "obj3" };
var callback3 = obj1.func.call(obj3);
setTimeout(callback3, 2000);
```

- callback2에서는 obj2의 func를 실행한 결과를 담아 이를 콜백으로 사용
- callback3의 경우 obj1의 func를 실행하면서 this를 obj3가 되도록 지정해 이를 콜백으로 사용
- this를 우회적으로나마 활용함으로써 다양한 상황에서 원하는 객체를 바라보는 콜백 함수를 만들 수 있는 방법

## 콜백 지옥과 비동기 제어

- `콜백지옥` : 콜백 함수를 익명 함수로 전달하는 과정이 반복되어 코드의 들여쓰기 수준이 감당하기 힘들 정도로 깊어지는 현상
- `비동기` : 동기의 반대말로, 현재 실행 중인 코드의 완료 여부와 무관하게 즉시 다음 코드로 넘어가는 것
  - 사용자의 요청에 의해 특정 시간이 경과되기 전까지 어떤 함수의 실행을 보류하거나(setTimeout)
  - 사용자의 직접적인 개입이 있을 때 비로소 어떤 함수를 실행하도록 대기한다거나(addEventListener)
  - 웹 브라우저 자체가 아닌 별도의 대상에서 무언가를 요청하고 그에 대한 응답이 왔을 때 비로소 어떤 함수를 실행하도록 대기하는 등 (XMLHttpRequest)
  - **별도의 요청, 실행 대기, 보류 등**

#### 콜백지옥 예시

```js
setTimeout(
  function (name) {
    var coffeeList = name;
    console.log(coffeeList);

    setTimeout(
      function (name) {
        coffeeList += "," + name;
        console.log(coffeeList);

        setTimeout(
          function (name) {
            coffeeList += "," + name;
            console.log(coffeeList);

            setTimeout(
              function (name) {
                coffeeList += "," + name;
                console.log(coffeeList);
              },
              500,
              "카페라떼"
            );
          },
          500,
          "카페모카"
        );
      },
      500,
      "아메리카노"
    );
  },
  500,
  "에스프레소"
);
```

#### 콜백지옥 해결 - 기명함수로 변환

```js
var coffeeList = "";

var addEspresso = function (name) {
  cofffeeList = name;
  console.log(coffeeList);
  setTimeout(addAmericano, 500, "아메리카노");
};

var addAmericano = function (name) {
  cofffeeList = "," + name;
  console.log(coffeeList);
  setTimeout(addMocha, 500, "카페모카");
};

var addMocha = function (name) {
  cofffeeList = "," + name;
  console.log(coffeeList);
  setTimeout(addLatte, 500, "카페라떼");
};

var addLatte = function (name) {
  cofffeeList = "," + name;
  console.log(coffeeList);
};
setTimeout(addEspresso, 500, "에스프레소");
```

- 코드의 가독성
- 함수 선언과 함수 호출만 구분할 수 있다면 위체서 부터 아래로 순서대로 읽어내려가는데 어려움 ❌
- 변수를 최상단으로 끌어올림으로써 외부에 노출되게 됐지만 전체를 즉시 실행 함수 등으로 감싸면 간단히 해결

- 코드명을 일일이 따라다녀야므로, 오히려 헷갈릴 소지 ⭕️

#### 비동기 작업의 동기적 표현 - Promise

```js
new Promise(function (resoleve) {
  setTimeout(function () {
    var name = '에스프레소';
    console.log(name);
    resolve(name);
  }, 500);
}).then(function(prevName) {
  return new Promise(function (resolve) {
    setTimeout(function() {
      var name = prevName + ', 아메리카노';
      console.log(name);
      resolve(name);
    },500);
  });
}).then(function(prevName) {
  return new Promise(function (resolve) {
    setTimeout(function() {
      var name = prevName + ', 카페모카';
      console.log(name);
      resolve(name);
    },500);
  }).then(function(prevName) {
  return new Promise(function (resolve) {
    setTimeout(function() {
      var name = prevName + ', 카페라떼';
      console.log(name);
      resolve(name);
    },500);
  });
});
```

- ES6의 Promise를 이용한 방식
- new 연산자와 함께 호출한 Promise의 인자로 넘겨주는 콜백 함수는 호출할 때 바로 실행되지만 그 내부에 resolve 또는 reject 함수를 호출하는 구문이 있을 경우 둘 중 하나가 실행되기 전까지 다음(then) 또는 오류(catch)로 넘어가지 않음
- 비동기 작업이 완료될 때 비로소 resolve 또는 reject를 호출하는 방법
- `비동기 작업의 동기적 표현이 가능`

#### 비동기 작업의 동기적표현 - Promise(2)

```js
var addCoffee = function (name) {
  return function (prevName) {
    return new Promise(function (resolve) {
      setTimeout(function () {
        var newName = prevName ? prevName + "," + name : name;
        console.log(newName);
        resolve(newName);
      }, 500);
    });
  };
};
addCoffee("에스프레소")()
  .then(addCoffee("아메리카노"))
  .then(addCoffee("카페모카"))
  .then(addCoffee("카페라떼"));
```

#### 비동기 작업의 동기적 표현 - Generator

```js
var addCoffee = function (prevName, name) {
  setTimeout(function () {
    coffeeMaker.next(prevName ? prevName + "," + name : name);
  }, 500);
};
var coffeeGenerator = function* () {
  var espresso = yield addCoffee("", "에스프레소");
  console.log(espresso);
  var americano = yield addCoffee(espresso, "아메리카노");
  console.log(americano);
  var mocha = yield addCoffee(americano, "카페모카");
  console.log(mocha);
  var latte = yield addCoffee(mocha, "카페모카");
  console.log(latte);
};
var coffeeMaker = coffeeGenerator();
coffeeMaker.next();
```

- '\*'이 붙은 함수가 바로 Generator 함수
- Generator 함수를 실행하면 Iterator가 반환, Iterator는 next라는 메서드 소유
- next 메서드를 호출하면 Generator 함수 내부에서 가장 먼저 등장하는 yield에서 함수의 실행 중단
- 비동기 작업이 완료되는 시점마다 next 메서드를 호출해준다면 Generator 함수 내부의 소스가 위에서부터 아래로 순차적으로 진행

#### 비동기 작업의 동기적 표현 - Promise + Async/await

```js
var addCoffee = function (name) {
  return new Promise(function (resolve) {
    setTimeout(function () {
      resolve(name);
    }, 500);
  });
};
var coffeeMaker = async function () {
  var coffeeList = "";
  var _addCoffee = async function (name) {
    coffeeList += (coffeeList ? "," : "") + (await addCoffee(name));
  };
  await _addCoffee("에스프레소");
  console.log(coffeeList);
  await _addCoffee("아메리카노");
  console.log(coffeeList);
  await _addCoffee("카페모카");
  console.log(coffeeList);
  await _addCoffee("카페라떼");
  console.log(coffeeList);
};
coffeeMaker();
```

- ES2017에서 가독성이 뛰어나면서 작성법도 간단한 새로운 기능 추가 => `async/await`
- 비동기 작업을 수행하고자 하는 함수 앞에 `async` 표기
- 함수 내부에서 실질적인 비동기 작업이 필요한 위치마다 `await`를 표기
  - 뒤의 내용을 Promise로 자동 전환
  - 해당 내용이 resolve 된 이후에야 다음으로 진행
- Promise의 then과 흡사한 효과

> 참고 : 코어 자바스크립트(Core JavaScript), 정재남
