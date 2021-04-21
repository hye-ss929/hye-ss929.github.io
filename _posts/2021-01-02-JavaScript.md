---
layout: post
title: Javascript - Array
date: 2021-01-02
tags: [JavaScript]
---

## 자료구조

- 비슷한 타입의 데이터(object)들을 묶어서 한곳에 보관해 놓는 것
- 어떤 방식/형식으로 데이터를 담냐에 따라서 굉장히 많은 타입이 존재
- 객체는 서로 연관된 특징과 행동들을 묶어 놓은것들을 의미 (자료구조와 다름)
- 삽입, 검색, 정렬, 삭제를 고려해서 자료구조중 가장 효율적인 것을 사용하는것이 중요
- 자료구조중 하나가 배열

### 1. 배열 선언 방법(Declaration)

```jsx
const arr1 = new Array();
const arr2 = [1, 2];
```

### 2. 인덱스 접근 방법 (Index position)

```jsx
const fruits = ["🍎", "🍌"];
console.log(fruits);
console.log(fruits.length);
console.log(fruits[0]);
console.log(fruits[1]);
console.log(fruits[fruits.length - 1]); //배열의 가장 마지막
```

### 3. 배열 반복(Looping over an array)

1. for

```jsx
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

2. for of

```jsx
for (let fruit of fruits) {
  console.log(fruit);
}
```

3. forEach(callback 함수를 받아옴)
   > forEach(callbackfn: (value: T, index: number, array: T[]) => void, thisArg?: any): void;

- callback함수 인자는 3가지 - value , index, array
- thisArg? 되어있으면 파라미터를 전달해도 되고 안해도 됨

```jsx
fruits.forEach(function (fruit, index, array) {
  console.log(fruit, index, array);
});

//보통 anonymous function일 경우, arrow 함수로 표기 가능
fruits.forEach((fruit) => console.log(fruit));
```

### 4. 배열 추가 / 삭제 / 복사 (Addtion, deletion, copy)

1. push : 배열 끝에 추가

```jsx
fruits.push("🍋", "🍇", "🍓");
console.log(fruits);
```

![](https://images.velog.io/images/hyehye/post/eb8c4f95-a904-492a-afe3-176d448fbb64/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-30%20%EC%98%A4%EC%A0%84%2011.56.18.png) 2) pop : 끝에서 배열 제거

```jsx
fruits.pop();
console.log(fruits);
```

![](https://images.velog.io/images/hyehye/post/1fb857f7-ffbb-4fdb-972b-eebc05a724a0/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-30%20%EC%98%A4%EC%A0%84%2011.56.27.png) 3) unshift : 배열 맨앞에 추가

```jsx
fruits.unshift("🍒", "🍑");
console.log(fruits);
```

![](https://images.velog.io/images/hyehye/post/a54ff487-dc0c-4cf8-b0f2-ad10565e1032/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-30%20%EC%98%A4%EC%A0%84%2011.56.57.png) 4) shift : 배열 첫요소 제거

```jsx
fruits.shift();
console.log(fruits);
```

![](https://images.velog.io/images/hyehye/post/eee9162c-10e6-443f-ab2d-5267f46efb39/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-30%20%EC%98%A4%EC%A0%84%2011.57.14.png)

- unshift와 shift는 배열을 수정하기 위해 첫번째 값을 두번째 배열로 옮긴 다음 첫번째 배열에 값을 넣기 때문에 시간이 소요됨.

5. concat : 여러개의 array 합치기

```jsx
const fruits2 = ["🍊", "🍍"];
const newFruits = fruits.concat(fruits2);
console.log(newFruits);
```

![](https://images.velog.io/images/hyehye/post/64b2d634-da55-4a27-b554-91f0a11e5d4a/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-30%20%EC%98%A4%EC%A0%84%2011.57.31.png)

### 5. 검색(Searching)

1. indexOf

```jsx
console.log(fruits);
console.log(fruits.indexOf("🥝"));
console.log(fruits.indexOf("🍇"));
```

2. includes : 특정 문자열 포함 여부

```jsx
console.log(fruits.includes("🍋"));
console.log(fruits.includes("🍎"));
```

![](https://images.velog.io/images/hyehye/post/59fb748b-cdfa-4427-bdc3-a33df30b03e0/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202020-12-30%20%EC%98%A4%EC%A0%84%2011.57.49.png) 3) lastIndexOf

```jsx
fruits.push("🍑");
console.log(fruits);
console.log(fruits.indexOf("🍑"));
console.log(fruits.lastIndexOf("🍑"));
```

> 출처 : 드림코딩 by 엘리 https://youtu.be/yOdAVDuHUKQ
