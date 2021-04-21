---
layout: post
title: TypeScript의 기본타입
date: 2021-03-18
tags: [TypeScript]
excerpt: TypeScript의 기본타입
---

#### JavaScript

- primitive (더이상 작은 단위로 나눠질 수 없는 타입)
  : number / string / boolean / null / undefined / symbol
- Object
  : function / array ...

### ✨Number

```tsx
let num: number = -3;
let hex: number = 0xf00d;
```

### ✨String

```tsx
let text:string = 'hello world";
let str:string = "-3";
```

### ✨Boolean

```tsx
let or: boolean = false;
```

### ✨Null과 Undefined

```tsx
let n: null = null;
let u: undefined = undefined;
```

- 단독적으로 사용하지는 않는 타입

```tsx
let n: numll | number;
let u: undefined | string;
```

### ✨Any

- 알지 못하는 타입을 표현해야 할 때 사용
- 기존의 JavaScript로 작업할 수 있는 강력한 방법

```tsx
let anything: any = 1;
anything = "hi";
anything = true;
```

### ✨Void

- 어떤 타입도 존재할 수 없음을 나타냄
- any의 반대 타입
- 아무것도 리턴하지 않을 때 사용

```tsx
function nothing(): void {
  console.log("nothing");
}

// 변수에는 null 또는 undefined만 할당 가능!
let unusable: void = undefined;
unusable = null;
```

### ✨Never

- 절대 발생할 수 없는 타입을 표현
- 함수표현식이나 화살표 함수 표현식에서 항상 오류를 발생시키거나 절대 반환하지 않는 반환타입

```tsx
function error(message: string): never {
  throw new Error(message);
}
```

### ✨Object

- 원시타입을 제외한 모든 타입 할당 가능

```tsx
function create(o: object | null) : void;
create({prop:0});
```
