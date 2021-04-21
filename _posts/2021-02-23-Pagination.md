---
layout: post
title: React - Pagination
date: 2021-02-23
tags: [React]
excerpt: Pagination
---

# Pagination

### 개념

리스트에서 데이터를 한번에 가져오는 것이 아니라 필요한 만큼, 또는 화면에 보이는 만큼만 백엔드에 요청하고 응답받아 사용하는 것을 의미

### ✨ Pagnation은 프론트엔드, 백엔드 양쪽에서 모두 구현

👉🏻 프론트엔드 : 현재의 위치(Offset)과 추가로 보여줄 컨텐츠의 수(Limit)를 백엔드에 전달
👉🏻 백엔드 : 그에 해당하는 데이터를 끊어 보내주는 방식으로 구현

### 이 과정에서 ❗️쿼리스트링❗️ 사용

👉🏻 해당 엔드포인트에 대해 질의문(query)를 보내는 요청

```
localhost:8000/product?limit=10&offset=5
```

➡️ "limit이 10이면서 offset이 5일 경우의 product 페이지를 보여달라"는 요청으로 해석

### ✅ 페이지네이션의 parameter

- limit : 한 페이지에서 보여줄 데이터 수
- offset : 데이터가 시작하는 위치(index)
- url에서 ? 기호는 유일무이
- parameter=value 로 필요한 파라미터의 값을 작성
- 파라미터가 여러개일 경우 &를 붙여서 여러개의 파라미터를 전달
