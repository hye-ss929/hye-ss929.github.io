---
layout: post
title: JavaScript - Array 활용
date: 2021-01-16
tags: [JavaScript]
---

### 1. 배열

배열을 사용하면 하나의 변수에 모든 데이터를 갖고 있을 수 있으며, `[](대괄호)`로 감싸져 있다.

```jsx
let arr = []; // 데이터가 없는 빈 배열
let cities = ["서울", "대전", "대구", "부산", "광주", "제주도"];
//요소 자리에는 문자열, 숫자열, 배열 모두 가능하다.
let anything = ["대전", 1987, ["하나", "둘", 3]];
```

### 2. 인덱스

인덱스를 통해 배열에 접근할 수 있다.

```jsx
let anything = ["대전", 1987, ["하나", "둘", 3]];
//
anything[0]; // 대전
anything[1]; // 1987
anything[2]; //['하나','둘',3]
```

### 3. 활용

1. 배열이 담긴 arr 변수에 접근하여 getElement 함수가 "array" 라는 문자열을 return 할 수 있도록 해주세요.

```jsx
//문제
function getElement() {
  let arr = [3, [4, ["array", 9], 2 + 3], [0]];
}

//풀이
function getElement() {
  let arr = [3, [4, ["array", 9], 2 + 3], [0]];
  return arr[1][1][0];
}
```

이 문제는 배열 속에 들어있는 여러가지 요소 중 "array"만을 return해야 한다.

인덱스를 통하여 "array"가 들어있는 배열에 접근하려 한다.

```jsx
return arr[1];
```

인덱스는 0은 3이며, 인덱스 1은 아래와 같다.
![](https://images.velog.io/images/hyehye/post/f2cdff21-24d4-4942-94a6-68056b24130a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.48.52.png)

이 배열에서 array가 들어있는 인덱스는 1임으로 다시 인덱스[1]를 불러온 뒤 값은 아래와 같다.
![](https://images.velog.io/images/hyehye/post/3c670b5b-e7dd-4e2e-990a-3181ff7b5ea2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.50.24.png)

마지막으로 인덱스[0]에 접근하게 되면 "array"만 return되는 것을 볼 수 있다.
![](https://images.velog.io/images/hyehye/post/5a201d5c-ec94-42ed-a653-635a17aaf653/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.51.49.png)

2.

```
//문제
- addFirstAndLast 함수 안에 작성해주세요.
- addFirstAndLast 함수에 주어진 인자 `myArray`는 숫자 값으로만 이루어진 array 입니다.
- addFirstAndLast 함수에 주어진 인자 `myArray` 의 첫번째 element와 마지막 element의 값을 더한 값을 리턴해주세요.
- 만일 `myArray`에 한 개의 요소만 있다면 해당 요소의 값을 리턴해 주시고 요소가 없는 비어있는 array라면 0을 리턴해주세요.
```

이 문제는 length를 사용하여 풀 수 있다.

```jsx
function addFirstAndLast(myArray) {
  if (myArray.length === 0) {
    return 0;
  } else if (myArray.length === 1) {
    return myArray[0];
  } else {
    return myArray[0] + myArray[myArray.length - 1];
  }
}
```

빈 배열의 길이는 0이므로 0 그대로 리턴을 하고, 배열이 하나 있을 경우 인덱스는 0부터 시작함으로 `myArray[0]`을 리턴한다.
문제에서 myArray의 첫번째 요소와 마지막 요소를 더하라 했기에 첫번째 요소를 `myArray[0]`로 불러오고, 마지막 요소는 `myArray.length-1`으로 배열의 가장 마지막을 불러와서 더해줄 수 있다.
