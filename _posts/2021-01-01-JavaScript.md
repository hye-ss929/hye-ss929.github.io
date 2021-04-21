---
layout: post
title: Javascript - Class · Object
date: 2021-01-01
tags: [JavaScript]
---

## < Class >

- object(인스턴스)를 만들 수 있는 틀이다.
- template(틀만을 정의해서 한번만 선언한다.)
- class 자체에 data가 들어있지 않다.
- class는 정의만 한 것이라 실제 메모리에는 올라가지 않는다.

### 1. Class 선언

```jsx
class Person {
  //constructor (생성자)
  constructor(name, age) {
    //fields
    this.name = name;
    this.age = age;
  }

  //methods
  speak() {
    console.log(`${this.name}: hello!`);
  }
}

const hyesung = new Person("hyesung", 24);
console.log(hyesung.name);
console.log(hyesung.age);
hyesung.speak();
```

![](https://images.velog.io/images/hyehye/post/79a39b93-316e-4bfb-affd-8ad3d5abab07/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-28%20%EC%98%A4%ED%9B%84%204.24.31.png)

### 2. Getter and Setters

> 💡 사용자가 class를 잘못 사용해도 방어적인 자세로 만들수 있도록 해주는 것

```jsx
class User {
  constructor(firstName, lastName, age) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age; //getter와 setter가 정의되어 있는 경우 자동으로 getter,setter 호출
  }

  get age() {
    return this._age; //기존의 age사용시 무한호출
  }

  set age(value) {
    this._age = value < 0 ? 0 : value; // 사용자의 입력값 검사
  }
}

const use1 = new User("Steve", "Job", -1); //나이를 -1로 잘못 설정시
console.log(use1.age);
```

### 3. Inheritance (상속)

- 한 클래스에서 다른 클래스로 확장하고자 할 때
- 공통되어지는 값들을 extends 키워드로 재사용 할 수 있다

### 4. Polymorphism(다형성)

- 필요한 메소드를 재정의해서 사용할 수 있다(오버라이딩)
- 오버라이딩 한 상태에서 부모 class의 메서드를 사용하고 싶으면 super 키워드를 사용

```jsx
class Shape {
  constructor(width, height, color) {
    this.width = width;
    this.height = height;
    this.color = color;
  }

  draw() {
    console.log(`drawing ${this.color} color!`);
  }

  getArea() {
    return this.width * this.height;
  }
}
class Rectangle extends Shape {} //상속을 통해 정의하는 방법
class Triangle extends Shape {
  draw() {
    super.draw(); //super : 재정의 시, 부모의 method까지 호출
    console.log("🔺");
  }
  //다형성 : 필요한 특정함수만 재정의
  getArea() {
    return (this.width * this.height) / 2;
  }
}
const rectangle = new Rectangle(20, 20, `Green`);
rectangle.draw();
console.log(rectangle.getArea());
const triangle = new Triangle(20, 20, `Blue`);
triangle.draw();
console.log(triangle.getArea());
```

![](https://images.velog.io/images/hyehye/post/22b0f046-4c62-4235-abdd-6461af126600/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-28%20%EC%98%A4%ED%9B%84%204.45.20.png)

### 5. Class cheking: instanceOf

- instanceof 를 기준으로 왼쪽과 오른쪽 비교

```jsx
console.log(rectangle instanceof Rectangle); //True
console.log(triangle instanceof Rectangle); //False
console.log(triangle instanceof Triangle); //True
console.log(triangle instanceof Shape); //True
console.log(triangle instanceof Object); //True
```

![](https://images.velog.io/images/hyehye/post/cf4d5d6e-9774-47b1-9a61-3b13c44077db/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-28%20%EC%98%A4%ED%9B%84%204.47.54.png)

## < Object >

- object = { key : value }
- 자바스크립트의 객체는 key와 value로 구성된 property의 집합
- key는 접근할 수 있는 변수이고, value는 그에 해당하는 값

### 1. Literals and properties

- 'object literal' syntax : 변수를 지정하여 object생성

```jsx
const obj1 = {};
```

-'object constructor' syntax : 클래스를 이용하여 object 생성

```jsx
const obj2 = new Object();
```

```jsx
//object를 사용하지 않은 경우,
const name = "hyesung";
const age = 25;
print(name, age);
function print(name, age) {
  console.log(name);
  console.log(age);
}

//object를 사용한 경우,
const hyesung = { name: "hyesung", age: 25 };
function print1(person) {
  console.log(person.name);
  console.log(person.age);
}
print(hyesung);
```

### 2.Computed(계산된) properties

- 동적으로 key, value를 받아와야 할 때 사용
- 변수에 접근하는 방법은 .말고도 배열에서 데이터 받아오듯 []사용가능
- 단, [] 사용시 string으로 표현

```jsx
console.log(hyesung.name); //코딩하는 순간 key에 해당하는 값을 받아오고 싶을 때
console.log(hyesung["name"]); //정확히 어떤 key가 필요한지 모를 때(runtime에서 결정될 때)
hyesung["hasJob"] = false;
console.log(hyesung.hasJob);

function printValue(obj, key) {
  // console.log(obj.key); 키 값이 오브젝트에 정의 x
  console.log(obj[key]); //지정되지 않은 오브젝트를 key가 표현
}

printValue(hyesung, "name");
printValue(hyesung, "age");
```

### 3. Property value shorthand (단축 속성명)

- makePerson이라는 함수를 만들어서 값만 전달하면 object를 간단히 생성가능

```jsx
const person1 = { name: "bob", age: 2 };
const person2 = { name: "steve", age: 3 };
const person3 = { name: "dave", age: 4 };
const person4 = makePerson("john", 30);
console.log(person4);

function makePerson(name, age) {
  return {
    name, //key와 value의 이름이 동일하다면 생략가능
    age,
  };
}
```

### 4. Constructor Function (생성자 함수)

```jsx
function Person(name, age) {
  //this = {}; 표현을 생략
  this.name = name;
  this.age = age;
  //return this; 표현을 생략
}
```

- 순수하게 오브젝트를 생성하는 함수는 대문자로 시작하고 return 쓰지 않고 class에서 constructor 했던 것처럼 this., 호출을 new Person 처럼 한다.

### 5. in operator : property existence check (key in obj) 해당하는 object 안에 key 유무

```jsx
console.log("name" in hyesung);
console.log("age" in hyesung);
console.log("random" in hyesung);
console.log(hyesung.random);
```

![](https://images.velog.io/images/hyehye/post/fbd64124-4314-42e0-8ccb-292f67a297c1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-12-29%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.07.50.png)

### 6. for..in vs for..of

- for (key in obj)

```jsx
for (let key in hyesung) {
  console.log(key);
}
```

- for (value of iterable)
  배열, 리스트에서 순차적으로 데이터가 담겨있는 것에서 사용

```jsx
//이전
for(let i = 0; i < array.lenght; i++) {
  console.log(array[i];);
}
// for of 사용
const array = [1, 2, 4, 5];
for(let value of array) {
    console.log(value);
}
```

### 7. Object.assign(dest, [obj1, obj2, obj3...])

- object 자체를 복사

```jsx
const user = { name: "popo", age: 5 };
const use2 = user;
use2.name = "coder";
console.log(user);

//방법1
const user4 = {};
Object.assign(user4, user);
console.log(user4);

//방법2
const user5 = Object.assign({}, user);
console.log(user5);
```

![](https://images.velog.io/images/hyehye/post/0cd2f141-15cb-402f-9868-071a86b978e8/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-12-29%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.12.29.png)

> 출처 : 드림코딩 by 엘리
> https://youtu.be/_DLhUBWsRtw
> https://youtu.be/1Lbr29tzAA8
