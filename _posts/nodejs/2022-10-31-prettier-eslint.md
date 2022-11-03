---
layout: single
author_profile: true
sidebar_main: true

title:  "[개발 환경 설정]Prettier, ESLint 설치 및 사용"

categories:
  - Nodejs
tags:
  - [JavaScript, npm, formatter, VSCode]

toc: true
toc_sticky: true
 
date: 2022-11-01
last_modified_at: 2022-11-03

comments: true
---

# Formatting과 Linting?

formatting은 세미콜론, space, quote등 코드의 아름다움..? 을 위해 지키는 것이라면,<br>
linting은 더 엄격한 코드 구조, 문법을 위해 사용한다.<br>
vscode에는 formatting과 linting을 위한 extension이 있는데 개발환경을 구축 할 때 많은 도움이 된다.<br>
올바른 코딩 습관을 형성하는데 도움을 주고, 협업 시에 코드를 청결하게 관리하는 데에 도움을 준다.

# Prettier

prettier는 세미콜론, 따옴표(쌍따옴표/홑따옴표)등의 룰을 정해서 자동으로 포맷해준다.

## Prettier 설치

vscode - extension에서 prettier를 먼저 설치하고 진행한다.

```shell
npm install --save-dev prettier
```

npm install 명령어로 prettier를 설치해준다.

## .prettierrc 작성

prettier를 사용하려면 prettier에 필요한 설정 파일을 생성해 줘야한다.<br>
root directory에 .prettierrc 파일을 생성해준다.

![1](https://user-images.githubusercontent.com/73820746/199729244-a53785f7-dd6e-4026-aaed-73ad7442b01b.png)

.prettierrc 파일은 json 형태로 작성한다.

```JSON
{
  "semi": true, // 세미콜론 쓸 것인지
  "singleQuote": true, // 문자열 리터럴을 표시할 때 작은따옴표로 쓸 것인지
} 	
```

## settings.json 작성

작성한 파일을 토대로 vscode가 prettier를 사용하도록 세팅해야한다.<br>
root directory에 .vscode 폴더를 만들고, 그 안에 settings.json 파일을 생성한다.

![2](https://user-images.githubusercontent.com/73820746/199729371-051ddbf6-faec-4b02-bb7a-74ff5e9ff135.png)

setting.json은 vscode가 하는 로컬 세팅을 모아놓는 곳이다.

즉 이 프로젝트에만 적용되는 세팅들을 모아놓는 곳이다.

```JSON
{
  "[javascript]": { // 자바스크립트 언어에 대해서 적용할 rule
    "editor.formatOnSave": true, // 저장 시 자동으로 지워줌.
    "editor.defaultFormatter": "esbenp.prettier-vscode" // plugin 이름
  }
}
```

# ESLint

ESLint는 안티패턴을 검증해준다.<br>

## ESLint 설치

vscode - extension에서 eslilnt를 먼저 설치하고 진행한다.

```shell
npm install --save-dev eslint
```

npm install 명령어로 eslint를 설치해준다. <br>

## .eslintrc.js 작성 

prettier처럼 eslint도 설정파일을 만들어준다. root directory에 .eslintrc.js 파일을 만들어준다.

```javascript
module.exports = {
  // eslint가 사용한 rule을 작성
};
```

rule을 하나하나 작성해도 되지만, 누군가가 이미 만들어서 정의해 놓은 rule을 가져와서 사용해도 된다.<br>
그 중에 airbnb의 eslint plugin을 설치해준다.

```bash
npm install --save-dev eslint-config-airbnb-base eslint-plugin-import
```

설치한 airbnb의 eslint config를 사용하기 위해 .eslintrc.js 파일에 적용해준다.

```javascript
module.exports = {
  extends: ['airbnb-base'],
};
```

## Prettier와 ESLint의 충돌 막기

Prettier는 세미콜론을 사용하라고 하고, ESLint는 세미콜론을 사용하지 말라고 한다면? <br>
둘이 충돌하는 경우를 막기 위해 사용하는 패키지를 설치한다.

```bash
npm install --save-dev eslint-config-prettier
```

.eslintrc.js 파일도 수정해준다.

```javascript
module.exports = {
  extends: ['airbnb-base', 'prettier'],
};
```

prettier는 항상 맨 뒤에 와야한다.

## ESLint 동작 막기

```javascript
/* eslint-disable-next-line */ // 다음 줄 코드에서 모든 ESLint 동작을 막는다.
console.log('hi'); // ESLint 동작 X

/* eslint-disable-next-line no-console */ // 다음 줄 코드에서 no-console 동작만 막는다.
console.log(eval()); // ESLint 동작하지만 console.log는 허용
```

## node 전용 plugin

```bash
npm install --save-dev eslint-plugin-node
```

설치하고 .eslintrc.js 수정

```jsx
module.exports = {
  extends: ['airbnb-base', 'plugin:node/recommended', 'prettier'],
};
```

깔끔한 코드를 짜기 위한 기본적인 세팅이다.