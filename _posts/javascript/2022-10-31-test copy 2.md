---
layout: single
author_profile: true
sidebar_main: true

title:  "var, const, let"

categories:
  - JavaScript

tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2022-11-05
last_modified_at: 2022-11-05

comments: true
---
<br>

# 💡 var, const, let의 차이점?

이전 자바스크립트에서 변수 선언은 var로 했다.<br>
ES6에서 const와 let이 추가되었다.

# hoisting

호이스팅(hoisting) 이란, 인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미한다.
var 변수 선언과 함수 선언문에서만 호이스팅이 일어난다.

```javascript
console.log(x); // undefined
var x = 1;
```

같은 scope 안에 x가 초기화 되어있기 때문에 undefined가 출력된다. 즉,

```javascript
var x;
console.log(x);
x = 1;
```

과 같은 것이다. hoisting은 결국 변수의 선언을 해당 스코프의 맨 위로 끌어 올리는 것이다.

```javascript
console.log(x);
x = 1; // reference error
```

위의 코드는 x가 선언이 되어있지 않기 때문에 에러이다.

```javascript
function foo() {
  return foo;
}

console.log(foo()); // foo
```

```javascript
console.log(foo()); // foo

function foo() {
  return foo;
}
```

function도 hoisting의 대상이다. 근데 함수는 왜 undefined가 출력되지 않았을까?<br>
함수의 선언과 값의 초기화는 서로 다르기 때문이다. 함수는 선언만 하고 초기화를 하지 않는다.

# binding

binding이란, 코드의 어떤 식별자가 실제로 어떤 값을 가리키는지 결정하는 것이다.

```javascript
function foo() {
  let x = 1;
  function bar() {
    console.log(x); // 1
  }
}
```

bar 안에 있는 x는 가장 가까운 스코프에서 일치하는 변수에 binding 된다.<br>
javascript 에서는 lexical scope를 통해 binding이 이루어진다.

> lexical scope : scope 안에서 바깥 쪽 변수에 접근 가능

```javascript
function foo() {
  var x = 'hello';
}
console.log(x); // reference error
```

lexical scope는 밖에서 안은 볼 수 없다.

```javascript
var x  = 1;
if (true) {
  var x = 2;
}
console.log(x); // 2
```

var는 block을 무시한다. 즉 block scoping에 영향을 받지 않는다.<br>
사실상 두개의 선언이 합쳐지게 되는 것이다.<br>

# let과 const

let과 const는 block scoping이고, hoisting 규칙이 없다. 그래서 var로 변수를 선언했을 때 보다 훨씬 예측 가능한 코드를 짤 수 있다

```javascript
let x = 1;
x = 2 // ok

const y = 1;
y = 2 // error

var z = 1;
var z = 2; // ok

let n = 1;
let n = 2; // syntax error
```

1. 같은 scope 내에서 같은 변수를 두 번 이상 정의할 수 없음.
2. 변수를 정의하기 전에는 사용할 수 없음.
3. scoping rule을 따름.

> ✏️ <br>
> let과 const의 예측 가능성과 유지 보수성이 var보다 훨씬 뛰어나다. <br>
> 변수 선언시에 가능하면 const만 쓰고, let은 필요한 경우에 쓰고, var는 절대 쓰지 말자!