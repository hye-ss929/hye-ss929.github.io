---
layout: post
title: 별점 기능 구현하기
date: 2021-07-04
tags: [JavaScript, React]
excerpt: 별점 기능 구현하기
---

토이프로젝트 중 별점 기능이 필요해졌다 !

라이브러리를 쓸까 하다가 이번에 제대로 알아두자 싶어서 직접 구현하였따..
정말 어려운 별점기능....................

### 1. 별의 개수 지정해주기!

<img src="https://images.velog.io/images/hyehye/post/f5c8ac3a-7450-43e0-9201-5c9feaf5ec71/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.14.26.png"/>

### 2. 별의 값을 가지고 있는 state 만들어주기

- 초기값은 props로 받아온 star로 초기화해주기
  <img src="https://images.velog.io/images/hyehye/post/a7e8b532-6e1b-4fde-8689-b7fdb24fd5f7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.41.44.png"/>
  <img src="https://images.velog.io/images/hyehye/post/1dabb4b0-5cd9-4f29-b534-550f49c02bb7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.15.46.png"/>

### 3. 별의 개수만큼 렌더링하기 위해 MAX_STAR만큼의 배열 만들기

1. 배열 생성하는 방법

   배열을 생성하는 방법은 다음과 같다
   <ul>1️⃣: `const arr = [요소1, 요소2]` // 배열 리터럴 이용</ul>
   <ul>2️⃣: `const arr = Array(요소1, 요소2)` // Array 객체의 생성자 이용</ul>
   <ul>3️⃣: `const arr = new Array(요소1, 요소2)` // new 연산자 이용</ul>

---

1️⃣번의 방법은 배열에 값을 따로 넣어줘야 하기 때문에 현재 별을 가지고 배열의 값을 넣어주는 건 비효율적이라 생각했다.

MAX_STAR=5만큼의 별을 만들기 위해 2️⃣과 3️⃣번을 이용해보았다.
<img src ="https://images.velog.io/images/hyehye/post/1f756816-7c33-4d29-9c07-7e9e7a7931e5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.08.18.png"/>

콘솔에 보니 이렇게 나왔다...

<img src="https://images.velog.io/images/hyehye/post/fb6384d3-0f26-4a1e-87f3-dcdc9b9189bd/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.08.59.png"/>

주어진 숫자만큼의 길이를 갖는 비어있는 배열이 나와버렸다.
그래서 배열를 n개 이상의 요소로 확장시킬 수 있는 스프레스 연산자를 활용해보았다.

<img src="https://images.velog.io/images/hyehye/post/3d6f8d3d-f67b-43f0-9c6e-862d7d60ccbf/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.12.31.png"/>

<img src="https://images.velog.io/images/hyehye/post/2afa6024-2612-400a-b32f-ae75e5d90e1b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.12.17.png"/>

....이렇게 나왔다..그래서 []를 이용해서 묶어보았다.

<img src="https://images.velog.io/images/hyehye/post/810eae1f-2c47-4ad4-91f6-14c15c27251e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.13.55.png"/>

<img src="https://images.velog.io/images/hyehye/post/95bdaae2-16cb-4719-a39c-0e15b2dfee6c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.14.02.png"/>

undefined가 5개들어간 배열이 드디어 나왔다. 이 배열을 돌면서 인덱스만 `<StarRating />`이라는 컴포넌트에 넘겨주었다.

### 4. 마우스 좌표 활용하기

마우스가 움직일 때마다 별이 가득 찼다가 빠졌다가 하기 때문에 좌표를 이용하려 하였다.

마우스 좌표에 대해 검색을 해보니 `getBoundingClientRect()` 이라는 메서드를 찾을 수 있었다.

`getBoundingClientRect()`는 엘리먼트를 감싸는 가장 작은 네모의 창 기준 좌표를 DOMRect 클래스의 객체형태로 반환환다.

<img src="https://images.velog.io/images/hyehye/post/c0b0622b-0a44-45ec-8927-2c831cc3865f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.32.16.png"/>

elem.getBoundingClientRect()의 각 프로퍼티를 그림으로 표현하면 다음과 같다.

<img src="https://images.velog.io/images/hyehye/post/d0319f28-67da-44d8-b191-5906ed8c5309/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.36.04.png"/>

이 이미지를 보면 현재 컴포넌트의 별이 있는 위치의 left는 529.5 이며 별이 들어간 컨텐츠의 width는 160임을 알 수 있다.

### 5. 클릭했을 때의 좌표 찾기

클릭했을 때의 좌표는 아래 사진처럼 웹페이지가 보이는 영역을 기준으로 하여 clientX의 값을 알 수 있다.

<img src="https://images.velog.io/images/hyehye/post/9100e1d1-e39f-4881-b109-fd890df73a5e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.47.16.png"/>

### 6. 마우스 위치 계산하기

<ul>1️⃣ : 웹 페이지에서 보이는 영역을 기준으로 `clientX` - 엘리먼트를 감싸는 가장 작은 네모의 창의 기준 좌표인 `getBoundingClientRect().left`를 빼면 엘리먼트를 감싸는 가장 작은 네모의 창부터 마우스가 위치한 곳의 값`x`을 계산 할 수 있다.</ul>

<ul>2️⃣ : 별 5개가 들어있는 컨텐츠의 길이는 앞서 계산한 width는 160이다. 이 width에는 별이 5개 들어가있기 때문에 MAX_STAR(5)로 나누어 주면 별 하나 당의 길이는 32이다. 또한 별 반개도 구하고 싶기 때문에 이를 다시 2로 나누면 별 반개의 width는 16이다.</ul>

<img src="https://images.velog.io/images/hyehye/post/8b85f449-f1ea-42d2-85f5-0e994e8a6041/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.02.18.png"/>

### 7. 별점 계산하기

엘리먼트를 감싸는 가장 작은 네모의 창부터 마우스가 위치한 곳의 값`x`를 별의 반개인 value를 16으로 나누면 최소 값인 0.5가 별의 반개, 1개가 별 한개인 별의 개수를 구할 수 있다.

단, 이렇게 계산했을 때에는 별을 다 체크하여도 9.8125로 10을 넘길 수 없기 때문에 +1를 하여 10으로 맞춰 준 다음 Math.floor를 이용하여 내림수를 구한 뒤 2로 나누어 최대값을 5로 맞출 수 있게 되는 것이다.

<img src="https://images.velog.io/images/hyehye/post/8d0700d8-cd3b-4785-8d6a-6683d42b77d0/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.19.31.png"/>

### 8. 별점 UI 구현하기

별이 들어간 컨텐츠에 onMouseMove 이벤트에 함수 handleMouseMove를 할당해준다.

함수 handleMouseMove는 이벤트를 받아 아까 만들어서 계산한 calculateStar함수에 이벤트를 전달해주고 이로 setstate인 setShowStar의 값을 변경해주는 작업을 할 수 있따

<img src="https://images.velog.io/images/hyehye/post/084cf212-6144-4c3c-a4d6-6362ab8eafa3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.25.55.png"/>

UI담당 StarRating 컴포넌트에 props로 showStar와 MAX_STAR만큼의 배열의 인덱스를 전달해준다

<img src="https://images.velog.io/images/hyehye/post/1c4f6ad3-caea-4b2d-aaec-b00772f2bee2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.27.47.png"/>

그런다음 이중삼항연산자을 통해 star가 i보다 크고, star - i 가 0.5 이면 반별을, 아니면 완전한 별을 보여주고, 아예 위 조건과 다를 시 빈별을 전달해준다.

<img src="https://images.velog.io/images/hyehye/post/5159a3f3-9e0a-4b41-b640-92816f93d394/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-07-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.33.52.png"/>

#### 💡 토이프로젝트 중 별점 미리보기

<img src="https://images.velog.io/images/hyehye/post/c7bd3c06-dc72-4440-b183-0bd019776d50/ezgif.com-gif-maker.gif"/>

### Refernece

[자바스트립트 요소의 절대좌표 상대좌표 구하기](https://mommoo.tistory.com/85)

[좌표](https://ko.javascript.info/coordinates)

[마우스 클릭 좌표](https://hianna.tistory.com/493)

[이중삼항연산자](https://harrislim.tistory.com/26)
