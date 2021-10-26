---
layout: post
type: re-born
date: 2021-10-21 16:53
category: Javascript
title: Modern JavaScript
subtitle: Node.js, 화살표 함수, 구조분해, 모듈화
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [Javascript, Node.js, Arrow Function, Destructing, CommonJS]
---



---



### Node.js

보통 사람들은 `Node.js`를 *서버를 만드는 환경*이나 *백엔드를 위한 환경*으로 잘못 이해하는 경우가 많다.

하지만 Node.js는 ***자바스크립트를 로컬에서 실행할 수 있도록 하는 환경***이다.

> **Package.json**
>
> `package.json`에는 프로그램을 실행시키기 위해 필요한 모듈, 방법, 테스트법 등이 명시되어 있다.
>
> 이 프로그램을 작동하기 위해 필요한 실제 모듈은 따로 `node_modules` 폴더에 저장되며, `package.json`에는 어떤 모듈인지만 적혀있다. (모듈 카탈로그/가이드 역할)
>
> `package.json`에는 아래와 같이 카테고리가 나뉘어 있다.
>
> - devDependencies : 프로그램 실행과 관계 없는, 오로지 개발을 위해 필요한 의존성 모듈
>
>   ```command
>   $ npm install (모듈명) --save-dev
>   ```
>
>   
>
> - dependencies : 프로그램을 직접 실행하기 위해 반드시 필요한 모듈
>
>   ```command
>   $ npm install react
>   또는
>   $ npm install --save react
>   ```
>
> 
>
> - scripts : CLI에서 사용 가능한 명령



### 화살표 함수

화살표 함수는 function 키워드를 화살표로 축약하여 표시하는 방법이다. (ES6부터 도입)

```js
const add = (x, y) => {
  return x + y;
}
```



화살표 함수는 본문에 return문만 있는 경우, return과 중괄호를 생략할 수 있다

```js
const add = (x, y) => x + y // correct
const add = (x, y) => {x + y} // error
const add = (x, y) => (x + y) // correct
```



만약, 함수 내의 표현식이 2줄 이상일 경우에는 가독성을 위해 return을 생략하기보다는 명시해 주는것이 좋다

```js
// bad
const getStudentAvg = arr => arr.filter(person => person.job === 'student').reduce((sum, person) => (sum + person.grade), 0)

// good
const getStudentAvg = arr => {
  return arr
    .filter(person => person.job === 'student')
    .reduce((sum, person) => (sum + person.grade), 0)
}
```





#### 활용법

화살표 함수는 클로저를 표현할 때 더욱 강력하다. 아래와 같은 함수 표현식이 있다고 가정할 때

```js
const adder = function(x) {
  return function(y) {
    return x + y
  }
}

adder(5)(7) // 12
```



화살표함수를 이용하면 아래와 같이 축약할 수 있다

```js
const adder = x => y => x + y
```

이와 같이 클로저는 연속된 여러 개의 화살표로 표시할 수 있다.







