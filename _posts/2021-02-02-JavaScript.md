---
layout: post
title: JavaScript - map & key props
date: 2021-02-02
tags: [JavaScript]
excerpt: map & key props
---

# Array.map

- 자바스크립트 배열 객체의 내장 함수
- 반복되는 컴포넌트의 렌더링 가능
- 파라미터로 전달된 함수를 사용하여 배열 내 각 요소를 원하는 규칙에 따라 변환한 후 그 결과로 새로운 배열에 저장

## key

- 리액트에서 key는 컴포넌트 배열을 렌더링했을 때, 어떤 항목에 변동이 있었는지를 알아내려고 사용한다.
- 유동적인 데이터 -> 생성 or 제거 or 수정 가능

## key 설정

- key 값을 설정할 때는 map함수의 인자로 전달되는 함수 내부에서 컴포넌트 props를 설정하듯이 설정

```jsx
<div>
  {commentArr.map((comment) => {
    return (
      <Comment
        key={comment.id}
        name={comment.userName}
        comment={comment.content}
      />
    );
  })}
</div>
```

- key의 값은 언제나 유일해야 한다
  => 데이터가 가진 고윳값을 key로 설정해야 한다.
