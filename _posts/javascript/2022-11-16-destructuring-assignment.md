---
layout: single
author_profile: true
sidebar_main: true

title:  "구조 분해 할당"

categories:
  - JavaScript

tags:
  - [JavaScript]

toc: true
toc_sticky: true
 
date: 2022-11-16
last_modified_at: 2022-11-16

comments: true
---
<br>

# 💡 구조분해 할당이란?

객채나 배열을 변수로 '분해'할 수 있게 해주는 문법이다.

## 배열을 변수로 분해하기
```javascript
var array = ['nodejs', {}, 10, true];
var node = array[0]; // 'nodejs'
var obj = array[1];  // {}
var bool = array[3]; // true

// 다음과 같이 바꿀 수 있다.
const array  = ['nodejs', {}, 10, true];
const [node, obj, , bool] = array;
```
인덱스를 이용해 배열에 접근하지 않아도 된다. 또한, 쉼표를 사용하여 필요하지 않은 배열 요소를 버릴 수 있다.

## 객체를 변수로 분해하기
> 기본문법
> ```javascript
> let {var1, var2} = {var1: ..., var2: ...}
> ```

할당 연산자 우측에는 분해하고자 하는 객체를, 좌측엔 상응하는 객체 프로퍼티의 '패턴'을 넣는다.

### Example 1
```javascript
let options = {
  title: 'Menu',
  width: 100,
  height: 200,
};

let { title, width, height } = options;

console.log(title); // Menu
console.log(width); // 100
console.log(height); // 200

// let 안의 순서가 바뀌어도 동일하게 동작함
let { height, width, title } = { title: 'Menu', height: 200, width: 100};
```






