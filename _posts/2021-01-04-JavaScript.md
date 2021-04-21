---
layout: post
title: Javascript - 유용한 10가지 배열함수들(join 외)
date: 2021-01-04
tags: [JavaScript]
---

Q1. 배열에서 문자열 만들기

- join() : 배열에 특정 구분자 넣어 문자형으로 변환하기

```jsx
const fruits = ["apple", "banana", "orange"];
const result = fruits.join(",");
console.log(result);
```

![](https://images.velog.io/images/hyehye/post/dc80b20b-b365-41b1-bd32-c58dd9e035be/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.21.03.png)

Q2. 문자열에서 배열 만들기

- split() : 문자열을 특정 구분자에 의해 배열로 나누기

```jsx
const fruits = "🍎, 🥝, 🍌, 🍒";
const result = fruits.split();
console.log(result);
```

![](https://images.velog.io/images/hyehye/post/5c802c07-926b-4e8a-a79c-e1e93c4d81c4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.21.35.png)

Q3. 배열을 다음과 같이 만들기 : [5, 4, 3, 2, 1]

- reverse() : 배열의 순서를 반대로 나열하기

```jsx
const array = [1, 2, 3, 4, 5];
const result = array.reverse();
console.log(result);
```

![](https://images.velog.io/images/hyehye/post/2c52a069-b785-4ae7-9251-629f37130bfe/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.21.55.png)

Q4. 처음 두 요소없이 새 배열 만들기

- slice() : 원하는 부분만 추출 (↔️ splice는 원배열을 바꾸기에 사용불가)

```jsx
const array = [1, 2, 3, 4, 5];
const result = array.slice(2, 5);
console.log(result);
```

![](https://images.velog.io/images/hyehye/post/664165d1-08f9-409c-a9ae-8c43c6a83a40/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.22.16.png)

<예제>

```jsx
class Student {
  constructor(name, age, enrolled, score) {
    this.name = name;
    this.age = age;
    this.enrolled = enrolled;
    this.score = score;
  }
}
const students = [
  new Student("A", 29, true, 45),
  new Student("B", 28, false, 80),
  new Student("C", 30, true, 90),
  new Student("D", 40, false, 66),
  new Student("E", 18, true, 88),
];
```

Q5. 점수가 90점인 학생 찾기

- find() : 배열의 특정 조건을 충족하는 요소 찾기

```jsx
//방법1.
const result2 = students.find((Student) => Student.score === 90);
console.log(result2);

//방법2.
const result3 = students.find(function (student) {
  return student.score === 90;
});
console.log(result3);
```

![](https://images.velog.io/images/hyehye/post/f61aece5-7582-4fa0-828f-6887975cd6d5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.22.38.png)

Q6. 등록한 학생만 출력하기

- filter() : 배열의 특정 조건을 기준으로 필터링하기

```jsx
//방법1.
const result4 = students.filter(function (student) {
  return student.enrolled === true;
});
console.log(result4);

//방법2
const result = students.filter((Student) => Student.enrolled === true);
console.log(result);
```

![](https://images.velog.io/images/hyehye/post/28d8bf0a-660d-4a19-bcc4-acbf59caba0a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.23.29.png)

Q7. 학생의 점수만 포함하는 배열 만들기: [45, 80, 90, 66, 88]

- map() : 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열 반환

```jsx
//방법1
const result = students.map((Student) => Student.score);
console.log(result);

//방법2
const result2 = students.map(function(student){
    return student.score;
    });
console.log(result2);
    }
```

![](https://images.velog.io/images/hyehye/post/703bfdc8-80af-4d61-852d-36ed9865be30/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.23.54.png)

Q8. 50 점 미만의 학생이 있는지 확인하기

- some() : 배열 요소가 특정 조건을 만족하는지 확인하기 (↔️ 모든 배열의 조건이 만족해야 할때는 every 사용)

```jsx
//방법1
const result = students.some((Student) => Student.score < 50);
console.log(result);

//방법2
const result2 = students.some(function (student) {
  return student.score < 50;
});
console.log(result2);
```

![](https://images.velog.io/images/hyehye/post/54b26187-6a41-4a8a-8fb0-93b98ce2c431/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.24.14.png)

Q9. 학생들의 평균 점수 계산

- reduce() : 배열의 각 요소를 하나씩 꺼내 사용자의 함수를 적용시킨 뒤, 그 값을 계속해서 누적시키는 함수

```jsx
const result = students.reduce((prev, curr) => {
  console.log("-----");
  console.log(prev);
  console.log(curr);
  return prev + curr.score; //return값 필수
}, 0); // initial값을 지정해주면 0에서 부터 시작
console.log(result / students.length);
```

![](https://images.velog.io/images/hyehye/post/7e3c4306-6609-409f-bf3e-9333c127188b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.24.39.png)

Q10. 모든 점수를 포함하는 문자열 만들기 : '45, 80, 90, 66, 88'

```jsx
const result = students.map((student) => student.score).join();
console.log(result);
```

![](https://images.velog.io/images/hyehye/post/d5aabf9f-1c06-4c4c-8e55-df1d4122018a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.25.11.png)

Q+.낮은 점수대로 정렬한 후 문자열로 변환 : '45, 66, 80, 88, 90'

- sort() : 배열 정렬

```jsx
const result = students
  .map((student) => student.score)
  .sort((a, b) => a - b) // 오름차순 ( b - a는 내림차순)
  .join();
console.log(result);
```

![](https://images.velog.io/images/hyehye/post/38d54fec-cdf3-429d-9576-a4a26b4cdd09/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.25.26.png)

> 출처 : 드림코딩 by 엘리 https://youtu.be/3CUjtKJ7PJg
