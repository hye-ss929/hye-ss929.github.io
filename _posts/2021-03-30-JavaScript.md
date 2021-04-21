---
layout: post
title: replace
date: 2021-03-30
tags: [JavaScript]
excerpt: replace method(모든 문자열 치환하기)
---

# replace

자바스크립트에서 어떤 패턴에 일치하는 일부 또는 모든 부분을 교체된 새로운 문자열을 반환하기 위해 `replace`를 사용한다.

이는 내가 배열에서 문자열로 바꾼 뒤에 단어 사이사이에 콤마(,)가 찍혀있어 바꾸기 위해 사용하였다.

```jsx
text.list.toString().toUpperCase().replace(",", "");
```

처음에 이렇게 사용했더니, 맨 앞에 있는 단어만 콤마가 지워져있고 나머지는 그대로였다.
그래서 검색을 해보니 첫번째 문자열만 바뀌고 나머지 문자열을 바뀌지 않는다는 것❗️

어떤 패턴에 일치하는 일부 또는 모든 부분을 바꾸기 위해서는 🔥 정규식(regular expression) 🔥을 사용해야 한다!

### 🚀 정규식 사용법

- 정규식으로 찾으려는 문자열을 `/`로 감싸서, 파라미터로 들어가는 값이 정규식임을 알려주기
- 그리고 `/` 뒤에 `g`를 붙여주기 ex)/n/g,'h'
  - 여기에서 `g`는 global match의 의미로 사용!

```jsx
let str = "hi,nice,meet,you";
str.replace(/,/g, "-"); // hi-nice-meet-you 출력
```
