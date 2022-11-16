---
layout: single
author_profile: true
sidebar_main: true

title:  "화살표 함수"

categories:
  - JavaScript

tags:
  - [JavaScript]

toc: true
toc_sticky: true
 
date: 2022-11-05
last_modified_at: 2022-11-05

comments: true
---
<br>

# 💡 화살표 함수(arrow function)란?

ES6에서 도입된 화살표 함수는 function 키워드 대신 화살표 => 를 사용해 좀 더 간략한 방법으로 함수를 선언할 수 있다. 화살표 함수는 항상 익명 함수로 정의한다.

```javascript
// 화살표 함수
const add = (x, y) => x + y;
console.log(add(2, 5)); // 7
```

화살표 함수는 기존의 함수 선언문 또는 함수 표현식을 완전히 대체하기 위해 디자인된 것은 아니다. 화살표 함수는 기존의 함수보다 표현만 간략한 것이 아니라 내부 동작 또한 간략화 되어있다.<br>
화살표 함수는 생성자 함수로 사용할 수 없으며, 기존 함수와 기존 binding 방식이 다르고, prototype 프로퍼티가 없으며 arguments 객체를 생성하지 않는다.

