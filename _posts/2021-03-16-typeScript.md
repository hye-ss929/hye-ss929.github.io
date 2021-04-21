---
layout: post
title: TypeScript
date: 2021-03-16
tags: [TypeScript]
excerpt: TypeScript
---

# TypdScript (타입스크립트)

- 마이크로소프트에서 구현한 JavaScript의 슈퍼셋 프로그래밍 언어
- .ts의 확장자를 사용하며, 컴파일의 결과물로는 JavaScript 코드 출력

↔️ JavaScript와의 차이점
✨ 정적 타입을 명시할 수 있다는 것

- 개발도구에게 개발자가 의도한 변수나 함수 등의 목적을 더욱 명확히 전달
- 잘못된 변수/함수 사용에 대한 에러 알림 등의 풍부한 피드백을 받을 수 있기에 어마어마한 생산성 향상
- "자바스크립트를 실제로 사용하기 전에 있을만한 타입 에러들을 미리 잡는 것"

↔️ JavaScript코드의 차이

```tsx
//javascript
const a = 3;
const b = "5";
console.log(a * b); //15 출력

//typescript
const a: number = 3;
const b: string = "5";
console.lgo(a * b); // Error ("The right-hand side of an arithmetic operation must be of type 'any', 'number', 'bigint' or an enum type.; 수리 연산의 우항 타입은 'any', 'number', 'bigint' 혹은 열거형이어야 합니다.")
```

🚀 개발 환경

- npm 설치 필수 ! 단, Node.js 설치하면 npm이 자동으로 설치!
- 터미널에 `npm i -g typescript` 입력 ➡️ 타입스크립트 컴파일러(타입스크립트 -> 자바스크립트 변환) 설치
- ex) script.ts 일 경우
  - 터미널에 `tsc script` 실행 ➡️ script.js 파일 생성
