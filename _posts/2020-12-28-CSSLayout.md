---
layout: post
title: CSS Layout
date: 2020-12-28
tags: [CSS]
---

## CSS의 레이아웃 정리

```html
<body>
  <!-- Block-level-->
  <div>div</div>
  <div>div</div>
  <div>div</div>

  <!--Inline-level-->
  <span>span</span>
  <span>span</span>
  <span>span</span>
</body>
```

```css
div, span{
  width:80px;
  height:80px;
  margin:20px;

div{
  background:red;
}

span{
  background:blue;
}
```

위와 같이 코드를 작성하여, 아래처럼 박스를 만들었다.

![](https://images.velog.io/images/hyehye/post/b99a3312-d08c-4bf6-95e8-d064a8cf39d3/1.png)

### 1. Display

(1) display:block

```css
span {
  background: blue;
  display: block;
}
```

Inline-level인 span에 display:block;을 주게 되면 블록(상자)처럼 상하로 배치된다.

![](https://images.velog.io/images/hyehye/post/035d9971-bc7d-4d19-a17d-0a7c999b0e3e/2.png)

(2) display:inline-block

```css
div {
  background: red;
  display: inline-block;
}
```

Block-level인 div에 display:inline-block;을 주게 되면 글자,상자의 특징을 모두 가져 한 줄에 여러개가 반영된다.

![](https://images.velog.io/images/hyehye/post/332c1db6-45ce-4302-bbad-34da7ffc577b/3.png)

(3) display:inline

```css
div {
  background: red;
  display: inline;
}
```

Block-level인 div에 display:inline;을 주게 되면 글자처럼 좌우로 배치된다.

![](https://images.velog.io/images/hyehye/post/7f8185c1-f505-4b04-9db4-01e64caf0d8f/4.png)

### 2. Position

```html
<body>
  <article class="container">
    <div></div>
    <div class="box">BOX</div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</body>
```

```css
div {
  width: 50px;
  height: 50px;
  margin-bottom: 20px;
  background: red;
}

.container {
  background: green;
  left: 20px;
  top: 20px;
}

.box {
  background: blue;
}
```

위와 같이 코드를 작성하여, 아래처럼 박스를 만들었다.

![](https://images.velog.io/images/hyehye/post/068ed65c-311c-462c-abc5-10ab2cb76cb9/5.png)

container에 left와 top에 값을 주어도 컨테이너의 이동이 없음을 알 수 있다.

이는 position에 기본으로 container에 left와 top에 값을 주어도 position에 static를 기본값으로 갖고 있기 때문이다.

(1) position: relative

```css
.container {
  background: green;
  left: 20px;
  top: 20px;
  position: relative;
}
```

![](https://images.velog.io/images/hyehye/post/98333116-ef73-49ea-b1d1-029ef81f97a2/6.png)

컨테이너position에 relative를 주니 left값과 top값이 적용된 것을 볼 수 있다.

```css
.box {
  background: blue;
  left: 20px;
  top: 20px;
  position: relative;
}
```

박스 position에 relative값을 주니, 원래 있어야 할 자리에서 left와 top값인 20px씩 옮겨 간 것을 볼 수 있다.

![](https://images.velog.io/images/hyehye/post/5e02554f-e00b-40fb-9683-f1b1e68d04b6/7.png)

(2) position: absolute

```css
.box {
  background: blue;
  left: 20px;
  top: 20px;
  position: absolute;
}
```

박스 position에 absolute값을 주면 상위 요소와 가까운 박스 안에서 위치변경이 일어나게 된다.

![](https://images.velog.io/images/hyehye/post/b75525d7-e096-480c-8d4e-5df1a914d0e1/8.png)

(3) position: fixed

```css
.box {
  background: blue;
  left: 20px;
  top: 20px;
  position: fixed;
}
```

![](https://images.velog.io/images/hyehye/post/a66d563b-41bd-4b73-af34-754c2e8aafb8/9.png)

박스 position에 fixed값을 주면 설정한 container 를 벗어나 윈도우를 기준으로 설정한 값의 위치변경이 일어나게 된다.

(4) position: sticky

```css
background:blue;
  left:20px;
  top:20px;
  position:sticky;
}
```

박스 position에 sticky값을 주면 원래 있어야 할 자리에 있으면서, 스크롤링 되어도 없어지지 않고 , 원래 자리에 고정되게 된다.

![](https://images.velog.io/images/hyehye/post/c985d193-98d6-4445-9d0b-719ace01f5bc/10.png)
