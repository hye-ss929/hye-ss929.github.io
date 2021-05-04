---
layout: post
title: Event
date: 2021-05-04
tags: [JavaScript]
excerpt: Event
---

![](https://images.velog.io/images/hyehye/post/79ed7432-89b8-4fe5-bb78-a67d9389b4c5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.31.38.png)

그림에서 볼 수 있듯이 html 문서는 차곡차곡 쌓여있다.
div를 클릭했을 때, div가 이벤트의 시발점(The Ultimate Cause)이다.

만약, div의 부모들에게도 click event가 있다면 부모들도 다같이 이벤트를 실행시켜버린다.
(div의 부모들에게도 click event가 없다면 아무 상관없는 문제이다)

### Event Flow

#### Event Bubblling (이벤트 버블링)

- 특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 상위 요소들로 전달되어 가는 특성

![](https://images.velog.io/images/hyehye/post/e9ec0f7f-2294-4dd1-ba74-6f0926b8079f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.06.12.png)

#### Event Capture (이벤트 캡쳐)

- Event Bubblling과는 반대로 진행되는 이벤트 전달 방식
- 클릭한 것은 하위에 있는 자식요소이지만 브라우저에서 제일 가까운 부모요소에서 자식요소의 순서로 이벤트가 실행 되는 것

![](https://images.velog.io/images/hyehye/post/12db4350-f0ef-44d7-8ae0-5be4834994c6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.15.47.png)

#### Target phase

- 이벤트의 진짜 target, 이벤트의 당사자가 실행되는 것

#### Current Target / Target

- `Current Target` : 이벤트의 진짜 주인
- `Target` : 이벤트의 시발점

`Target phase`만을 눌렀을 뿐인데, capture와 bubble이 중복으로 실행이 된다.
그래서 브라우저에서는 `target`과 `currentTarget`이 다르고, 상위 요소에서도 이벤트가 발생하는 상황에서는 `bubble`이 기본값이다.

![](https://images.velog.io/images/hyehye/post/37a23771-5ddd-49f8-a534-fdb1d9ee72b2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.45.46.png)

#### EventTarget.addEventListener()

- 기본값은 `bubble`이지만, addEventListener()의 세 번째 인자로 `ture`를 넣어주면 `capture`로 바꿀 수 있다.

```js
target.addEventListener(type, listener[, useCapture]);
```

### 이벤트 객체 메소드

#### e.stopPropagation()

- 이벤트 캡처링과 버블링에 있어 해당 이벤트가 전파되는 것을 막음

#### e.preventDefault()

- 이벤트를 취소할 수 있는 경우, 이벤트의 전파를 막지않고 그 이벤트를 취소함

### Event Delegation (이벤트 위임)

- 하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어하는 방식

```
<h1>To Do List</h1>
    <ul class="todolist">
      <li>
        <input type="checkbox" id="todo1">
        <label for="todo1">책읽기</label>
      </li>
      <li>
        <input type="checkbox" id="todo2">
        <label for="todo2">운동하기</label>
      </li>
      <li>
        <input type="checkbox" id="todo3">
        <label for="todo3">공부하기</label>
      </li>
    </ul>
```

```js
// javascript
const checkboxs = document.querySelectorAll("input");

checkboxs.forEach(function (checkbox) {
  checkbox.addEventListener("click", function (e) {
    alert("Done 🎉");
  });
});
```

![](https://images.velog.io/images/hyehye/post/23eb2974-7c4d-4147-8181-f4769407aef5/ezgif.com-gif-maker.gif)
모든 input에 클릭 이벤트를 줘서 체크박스를 클릭하면 alert가 뜨게끔 구현하였다.

이후 새로운 리스트를 추가하고, 똑같이 클릭해보았다.

```js
const todolist = document.querySelector(".todolist");
const li = document.createElement("li");
const input = document.createElement("input");
const label = document.createElement("label");
const innerText = document.createTextNode("일기쓰기");

input.setAttribute("type", "checkbox");
input.setAttribute("id", "todo4");
label.setAttribute("for", "todo4");
label.appendChild(innerText);
li.appendChild(input);
li.appendChild(label);
todolist.appendChild(li);
```

![](<https://images.velog.io/images/hyehye/post/3c7cae3e-df26-4314-aaaf-e495614e8f46/ezgif.com-gif-maker%20(1).gif>)
새로 추가한 리스트에는 클릭 이벤트가 제대로 작동하지 않는다.
이는 새로 추가된 리스트에 클릭 이벤트를 걸어주지 않았기 때문이다.

이럴 때 사용할 수 있는 방법은 바로 `이벤트 위임` 이다.
input에 이벤트를 걸어주는 것이 아닌 input의 상위 요소인 ul 태그에 이벤트를 걸어서, 하위에서 발생한 이벤트를 감지하게 한다.

```js
const todolist = document.querySelector(".todolist");
todolist.addEventListener("click", function (e) {
  alert("Done 🎉");
});
```

![](<https://images.velog.io/images/hyehye/post/b9029721-4861-4a50-ba6b-24973b028612/ezgif.com-gif-maker%20(2).gif>)

> [김버그의 DOM 이벤트 플로우 완벽하게 정리해드립니다.](https://youtu.be/7gKtNC3b_S8)

> [캡틴판교의 이벤트 버블링, 이벤트 캡처 그리고 이벤트 위임까지](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/#eventstoppropagation)
