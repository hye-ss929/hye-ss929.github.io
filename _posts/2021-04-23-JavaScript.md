---
layout: post
title: JavaScript - 클래스
date: 2021-04-23 04:53 +0800
tags: [JavaScript]
excerpt: JavaScript - 클래스
---

# 자바스크립트 - 클래스

자바스크립트는 프로토타입 기반의 언어라서 `상속`개념 존재 ❌

## 클래스와 인스턴스의 개념 이해

> **일반적인 개념으로서의 클래스**

```
음식(superClass) - 과일(subClass/superClass) - 귤류(subClass) - 오렌지(element)
```

- 하위 클래스가 아무리 구체화되더라도 결국 `추상적인 개념`
- 어떤 클래스의 속성을 지니는 실존하는 개체를 `인스턴스`라 함
- 클래스는 인스턴스들로부터 공정점을 발견하여 정의
- 하나의 개체가 같은 레벨의 서로 다른 여러 클래스의 인스턴스 일 수 있음

> **프로그래밍 언어상의 클래스**

- 사용자가 직접 여러 가지 클래스를 정의
- 클래스를 바탕으로 인스턴스를 만들 때 비로소 어떤 개체가 클래스 속성을 지님
- 클래스가 먼저 정의되어야만 그로부터 공통적인 요소를 지니는 개체들을 생성 가능
- 한 인스턴스는 하나의 클래스만을 바탕으로 생성(인스턴스를 생성할 때 호출할 수 있는 클래스는 오직 하나뿐일 수 밖에 없기 때문)
- 사용하기에 따라 추상적인 대상 또는 구체적인 개체

## 자바스크립트의 클래스

- 자바스크립트는 프로토타입 기반 언어이므로 클래스의 개념 존재 ❌
- 프로토타입을 일반적인 의미에서의 클래스 관점에서 접근해보면 비슷하게 해석할 수 있는 요소 ⭕️
  - 생성자 함수 Array를 new 연산자와 함께 호출하면 인스턴스 생성
  - 이때 Array를 일종의 클래스라 하면, Array의 prototype 객체 내부 요소들이 인스턴스에 "상속"된다 볼 수 있음(엄밀히는 상속이 아닌 프로토타입 체이닝에 의한 참조)
- Array 내부 프로퍼티들 중에 prototype 프로퍼티를 제외한 나머지는 인스턴스에 상속 ❌

👉🏻 인스턴스에 상속되는지(인스턴스가 참조하는지) 여부에 따라 **스태틱 멤버** / **인스턴스 멤버**로 구분

> 단, 자바스크립트에서는 인스턴스에서도 직접 메서드를 정의할 수 있기에 혼란을 야기할 수 있어서 인스턴스메서드 대신 **프로토타입 메서드**라 부는 것이 좋음

```js
// 생성자
var Rectangle = function (width, height) {
  this.width = width;
  this.height = height;
};

//(프로토타입) 메서드
Rectangle.prototype.getArea = function () {
  return this.width * this.height;
};

//스태틱 메서드
Rectangle.isRectangle = function (instance) {
  return (
    instance instanceof Rectangle && instance.width > 0 && instance.height > 0
  );
};

var rect1 = new Rectangle(3, 4);
console.log(rect1.getArea()); // 12 (0)
console.log(rect1.isRectangle(rect1)); // error(x)
console.log(Rectangle.isRectangle(rect1)); // true
```

- 프로토타입 메서드는 인스턴스가 마치 자신의 것처럼 호출할 수 있으므로,`rect1.__proto__.getArea`에 접근하는 것과 동일
  - 따라서 rect1.width \* rect1.height 계산값 반환
  - 이처럼 인스턴스에서 직접 호출할 수 있는 메서드가 바로 **프로토타입 메서드**
- rect1 인스턴스에서 isRectangle이라는 메서드에 접근하려 하지만, `rect1`에 해당 메서드는 없고, `rect1.__proto__`에도 없으며, `rect1.__proto__.__proto__(= Object.prototype)`에도 없음
  - 즉, 함수가 아니여서 실행할 수 없음(TypeError: rect1.isRectangle is not a function)
- 인스턴스에서 직접 접근할 수 없는 메서드를 **스태틱 메서드**라 함
- 스태틱 메서드는 생성자 함수를 마지막 줄처럼 this로 해야만 호출 가능

## 클래스 상속

### 클래스가 구체적인 데이터를 지니지 않게 하는 방법

- subClass.prototype에 superClass의 인스턴스를 할당한 다음 `프로퍼티를 모두 삭제`하는 방법
- subClass.prototype에 superClass의 인스턴스를 할당하는 대신 아무런 프로퍼티를 생성하지 않는 `빈 생성자 함수(Bridge)`를 활용하는 방법
- `Object.create`를 활용하는 방법(앞서 소개한 두 방법보다 간단하면서 안전)

### ES6의 클래스 및 클래스 상속

#### ES5와 ES6의 클래스 문법 비교

```js
//ES5
var ES5 = function (name) {
  this.name = name;
};
ES5.staticMethod = function () {
  return this.name + " staticMethod";
};
ES5.prototype.method = function () {
  return this.name + " method";
};
var es5Instance = new ES5("es5");
console.log(ES5.staticMethod()); // es5 staticMethod
console.log(es5Instance.method()); // es5 method
```

```js
//ES6
var ES6 = class {
  constructor(name) {
    this.name = name;
  }
  static staticMethod() {
    return this.name + " staricMethod";
  }
  method() {
    return this.name + " method";
  }
};
var es6Instance = new ES6("es6");
console.log(ES6.staticMethod()); //es6 staricMethod
console.log(es6Instance.method()); // es6 method
```

- `class`라는 명령어 뒤에 바로 `{}` 등장
  - 이 중괄호 묶음 내부가 클래스 본문 영역
- `constructor`라는 이름 뒤에 바로 `() {`가 등장
  - 클래스 본문에서는 'function' 키워드를 생략하더라도 모두 메서드로 인식
  - constructor 이름에서 바로 알 수 있듯이, ES5의 생성자 함수와 동일한 역할 수행
- 메서드와 다음 메서드 사이에는 콤마(,)로 구분하지 않음
- `static`이라는 키워드 뒤에 `staticMethod`라는 이름 등장했고, 뒤이어 `() {`가 등장
  - static 키워드는 해당 메서드가 static 메서드임을 알리는 내용
  - ES5체게에서 생성자 함수에 바로 할당하는 메서드와 동일하게 생성자 함수(클래스) 자신만이 호출
- `method`가 바로 나오는 부분은 자동으로 `prototype` 객체 내부에 할당되는 메서드
  - ES5.prototype.method와 동일하게, 인스턴스가 프로토타입 체이닝을 통해 마치 자신의 것처럼 호출할 수 있는 메서드

#### ES6의 클래스 상속

```js
var Rectangle = class {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  getArea() {
    return this.width * this.height;
  }
};
var Square = class extends Rectangle {
  constructor(width) {
    super(width, width);
  }
  getArea() {
    console.log("size is :", super.getArea());
  }
};
```

- `Square를 Rectangle` 클래스를 상속받는 SubClass로 만들기 위해 `class 명령어 뒤`에 단순히 'extends Rectangle' 내용 추가
  - 이것만으로 상속 관계 설정 끝
- `constructor` 내부에서는 `super`라는 키워드를 `함수`처럼 사용할 수 있는 데, 이 함수는 SuperClass의 constructor 실행
- `constructor` 메서드를 제외한 다른 메서드에서는 `super` 키워드를 마치 `객체`처럼 사용 가능
  - 이때 SuperClass.prototype을 바라보는데, 호출한 메서드의 this는 'super'가 아닌 원래의 this를 따름

> 참고 : 코어 자바스크립트(Core JavaScript), 정재남
