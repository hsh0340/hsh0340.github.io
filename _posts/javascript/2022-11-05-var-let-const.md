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

# ๐ก var, const, let์ ์ฐจ์ด์ ?

์ด์  ์๋ฐ์คํฌ๋ฆฝํธ์์ ๋ณ์ ์ ์ธ์ var๋ก ํ๋ค.<br>
ES6์์ const์ let์ด ์ถ๊ฐ๋์๋ค.

# hoisting

ํธ์ด์คํ(hoisting) ์ด๋, ์ธํฐํ๋ฆฌํฐ๊ฐ ๋ณ์์ ํจ์์ ๋ฉ๋ชจ๋ฆฌ ๊ณต๊ฐ์ ์ ์ธ ์ ์ ๋ฏธ๋ฆฌ ํ ๋นํ๋ ๊ฒ์ ์๋ฏธํ๋ค.
var ๋ณ์ ์ ์ธ๊ณผ ํจ์ ์ ์ธ๋ฌธ์์๋ง ํธ์ด์คํ์ด ์ผ์ด๋๋ค.

```javascript
console.log(x); // undefined
var x = 1;
```

๊ฐ์ scope ์์ x๊ฐ ์ด๊ธฐํ ๋์ด์๊ธฐ ๋๋ฌธ์ undefined๊ฐ ์ถ๋ ฅ๋๋ค. ์ฆ,

```javascript
var x;
console.log(x);
x = 1;
```

๊ณผ ๊ฐ์ ๊ฒ์ด๋ค. hoisting์ ๊ฒฐ๊ตญ ๋ณ์์ ์ ์ธ์ ํด๋น ์ค์ฝํ์ ๋งจ ์๋ก ๋์ด ์ฌ๋ฆฌ๋ ๊ฒ์ด๋ค.

```javascript
console.log(x);
x = 1; // reference error
```

์์ ์ฝ๋๋ x๊ฐ ์ ์ธ์ด ๋์ด์์ง ์๊ธฐ ๋๋ฌธ์ ์๋ฌ์ด๋ค.

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

function๋ hoisting์ ๋์์ด๋ค. ๊ทผ๋ฐ ํจ์๋ ์ undefined๊ฐ ์ถ๋ ฅ๋์ง ์์์๊น?<br>
ํจ์์ ์ ์ธ๊ณผ ๊ฐ์ ์ด๊ธฐํ๋ ์๋ก ๋ค๋ฅด๊ธฐ ๋๋ฌธ์ด๋ค. ํจ์๋ ์ ์ธ๋ง ํ๊ณ  ์ด๊ธฐํ๋ฅผ ํ์ง ์๋๋ค.

# binding

binding์ด๋, ์ฝ๋์ ์ด๋ค ์๋ณ์๊ฐ ์ค์ ๋ก ์ด๋ค ๊ฐ์ ๊ฐ๋ฆฌํค๋์ง ๊ฒฐ์ ํ๋ ๊ฒ์ด๋ค.

```javascript
function foo() {
  let x = 1;
  function bar() {
    console.log(x); // 1
  }
}
```

bar ์์ ์๋ x๋ ๊ฐ์ฅ ๊ฐ๊น์ด ์ค์ฝํ์์ ์ผ์นํ๋ ๋ณ์์ binding ๋๋ค.<br>
javascript ์์๋ lexical scope๋ฅผ ํตํด binding์ด ์ด๋ฃจ์ด์ง๋ค.

> lexical scope : scope ์์์ ๋ฐ๊นฅ ์ชฝ ๋ณ์์ ์ ๊ทผ ๊ฐ๋ฅ

```javascript
function foo() {
  var x = 'hello';
}
console.log(x); // reference error
```

lexical scope๋ ๋ฐ์์ ์์ ๋ณผ ์ ์๋ค.

```javascript
var x  = 1;
if (true) {
  var x = 2;
}
console.log(x); // 2
```

var๋ block์ ๋ฌด์ํ๋ค. ์ฆ block scoping์ ์ํฅ์ ๋ฐ์ง ์๋๋ค.<br>
์ฌ์ค์ ๋๊ฐ์ ์ ์ธ์ด ํฉ์ณ์ง๊ฒ ๋๋ ๊ฒ์ด๋ค.<br>

# let๊ณผ const

let๊ณผ const๋ block scoping์ด๊ณ , hoisting ๊ท์น์ด ์๋ค. ๊ทธ๋์ var๋ก ๋ณ์๋ฅผ ์ ์ธํ์ ๋ ๋ณด๋ค ํจ์ฌ ์์ธก ๊ฐ๋ฅํ ์ฝ๋๋ฅผ ์งค ์ ์๋ค

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

1. ๊ฐ์ scope ๋ด์์ ๊ฐ์ ๋ณ์๋ฅผ ๋ ๋ฒ ์ด์ ์ ์ํ  ์ ์์.
2. ๋ณ์๋ฅผ ์ ์ํ๊ธฐ ์ ์๋ ์ฌ์ฉํ  ์ ์์.
3. scoping rule์ ๋ฐ๋ฆ.

> โ๏ธ <br>
> let๊ณผ const์ ์์ธก ๊ฐ๋ฅ์ฑ๊ณผ ์ ์ง ๋ณด์์ฑ์ด var๋ณด๋ค ํจ์ฌ ๋ฐ์ด๋๋ค. <br>
> ๋ณ์ ์ ์ธ์์ ๊ฐ๋ฅํ๋ฉด const๋ง ์ฐ๊ณ , let์ ํ์ํ ๊ฒฝ์ฐ์ ์ฐ๊ณ , var๋ ์ ๋ ์ฐ์ง ๋ง์!