---
layout: post
title: JavaScript - Date 객체
date: 2021-01-17
tags: [JavaScript]
---

## Date 객체

Date 객체를 활용하면 생성 및 수정 시간을 저장하거나 시간을 측정할 수 있고 현재 날짜를 출력하는 용도 등으로 활용할 수 있다.

### 날짜 객체 생성하기

`new Date()`
: 현재시간 기준

```jsx
let now = new Date();
alert(now); // Fri Jan 15 2021 20:30:26 GMT+0900 (대한민국 표준시)
```

`new Date(milliseconds)`
: UTC 기준(UTC+0) 1970년 1월 1일 0시 0분 0초에서 밀리초 후 시점

`new Date(datestring)`
: 날짜를 표현하는 문자열 값

```jsx
let date = new Date("2017-01-26");
alert(date);
// 인수로 시간은 지정하지 않았기 때문에 GMT 자정이라고 가정하고
// 코드가 실행되는 시간대(timezone)에 따라 출력 문자열이 바뀝니다.
// 따라서 얼럿 창엔
// Thu Jan 26 2017 11:00:00 GMT+1100 (Australian Eastern Daylight Time)
// 혹은
// Wed Jan 25 2017 16:00:00 GMT-0800 (Pacific Standard Time)등이 출력됩니다.
```

`new Date(year, month, date, hours, minutes, seconds, ms)`

- year : 반드시 4자리 값
- month : 0(1월) ~ 11(12월)
- day : 기본값은 1
- hours, minutes, seconds, ms : 기본값은 0

### 날짜 얻기

`getFullYear()`
: 연도(YYYY) 반환
`getMonth()`
: 월 반환(getMonth 값을 받을 때, 현재 달보다 1 작은 값이 반환되므로 주의)
`getDate()`
: 일 반환
`getHours(), getMinutes(), getSeconds(), getMilliseconds()`
: 시, 분, 초, 밀리초 반환

#### getTime

- 날짜의 밀리초를 반환
- 시간이 지난 뒤 새로 호출하면 시간이 지났으니 보다 큰 숫자를 반환
- getTime함수로 비교연산을 통해 언제가 더 과거인지 판단가능(값이 더 작으면 과거)

#### 날짜 구성요소 설정

`setFullYear(year, [month], [date])`
: 현지 시간에 따라 지정된 날짜의 전체 연도 설정
: 반환값 → number, 지정한 시간을 1970년 1월 1일을 기준으로 하는 밀리세컨드로 리턴
`setMonth(month, [date])`
`setDate(date)`
`setHours(hour, [min], [sec], [ms])`
`setMinutes(min, [sec], [ms])`
`setSeconds(sec, [ms])`
`setMilliseconds(ms)`
`setTime(milliseconds)`
