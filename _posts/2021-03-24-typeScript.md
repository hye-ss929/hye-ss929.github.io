---
layout: post
title: Interface
date: 2021-03-18
tags: [TypeScript]
excerpt: TypeScript의 Interface
---

# Interface

- 타입들의 이름을 짓는 역할
- 코드 안의 계약을 정의
- 프로젝트 외부에서 사용하는 코드의 계약을 정의

```tsx
interface Age {
  age: number;
}

function personAge(personObj: Age) {
  console.log(personObj.key);
}

let person = { name: "job", age: 20 };
personAge(person);
```

- personAge는 Age의 타입을 가져야 한다.
- ✨ 인터페이스를 인자로 받아 사용할 때 인터페이스의 속성 갯수와 인자로 받는 객체의 속성 갯수를 일치시키지 않아도 된다.
- ✨ 함수에 전달된 객체가 나열된 요구 조건을 충족하면, 허용된다.

### 선택적 프로퍼티 (Optional Properties)

- 선택적 프로퍼티는 선언에서 프로퍼티 이름 끝에 `?`를 붙여 표시
- ✨ 즉, 있어도 되고 없어도 된다는 표시

```tsx
interface Student {
	name : string;
  	grade? : number;
}

let student1 = {
	name : 'bob';
};

function newStudent(student:Student){
	console.log(student.name);//bob
}
```

- ✨ `newStudent()` 함수에서 `student` 인터페이스를 인자의 타입으로 선언했지만, 인자로 넘긴 객체에는 `grade`가 없다 ➡️ `grade`를 선택적 프로퍼티로 선언했기 때문!

### 읽기전용 프로퍼티 (Read0nly properties)

- 프로퍼티 이름 앞에 `readonly`를 붙히게 되면 더이상 수정이 불가능해진다.

```tsx
interface Point {
  readonly x: number;
  readonly y: number;
}

let p1: Point = { x: 10, y: 20 };
p1.x = 8; //오류 - 불가능!
```

#### ReadonlyArray`<T>`

- 배열 선언 시, `ReadonlyArray<T>` 타입을 사용하면 읽기전용 배열 생성 가능

```tsx
let arr: number[] = [1, 2, 3, 4, 5];
let readNum: ReadonlyArray<number> = arr;

readNum[0] = 10; // 에러
readNum.push(8); // 에러
arr = readNum; // 에러
```

- `ReadonlyArray`를 일반 배열에 재할당 불가능

### 객체 선언과 관련된 타입 체킹 (Excess Property Checks)

```tsx
interface NewZoo {
  animal?: string;
  size?: number;
}

function createZoo(zoo: NewZoo) {
  //...
}

createZoo({ animel: "lion" }); // error: Object literal may only specify known properties, but 'animel' does not exist in type 'NewZoo'. Did you mean to write 'animal'?

let korZoo = { animel: "lion" };
```

`NewZoo` 인터페이스에는 `animal` 이라고 선언되어있지만 `createZoo()`함수에 인자로 넘기는 `korZoo` 객체에는 `animel`이 선언되어 있어 오탈자를 점검하라는 오류가 발생 💥

🚀 타입 추론을 무시하고 싶을 때 다음과 같이 선언

- `createZoo(korZoo as NewZoo)`
- 인터페이스 정의하지 않은 속성들을 추가로 사용하고 싶을 때

```tsx
interface NewZoo {
  animal?: string;
  size?: number;
  [propName: string]: any;
}
```

### 함수 타입 (Function Types)

- 함수의 타입을 정의할 때도 사용 가능

```tsx
interface login {
  (username: string, password: string): boolean;
}
```

- 함수의 인자의 타입과 반환 값의 타입 정의

```tsx
let loginUser: login;
loginUser = function (id: string, pw: string) {
  console.log("로그인 성공");
  return true;
};
```

### 인터페이스 확장 (Extending Interfaces)

```tsx
interface Person {
  name: string;
}

interface Developer extends Person {
  skill: string;
}

let he = {} as Developer;
he.name = "jack";
he.skill = "TypeScript";
```

- 여러 인터페이스를 확장할 수 있기에, 모든 인터페이스의 조합을 만들 수 있다.

```tsx
interface Hobby {
  hobby: string;
}

interface Developer extends Person, Hobby {
  isJob: boolean;
}

let he = {} as Developer;
he.hobby = fishing;
he.isJob = false;
```
