---
layout: post
type: re-born
date: 2021-10-16 22:28
category: Javascript
title: 고차함수
subtitle: map, filter, reduce
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [Javascript, 고차함수, map, filter, reduce]
---



---



### 고차함수

고차함수는 ***함수를 인자로 받거나, 함수를 리턴하는 함수***를 말한다.

(여기서 인자로 들어가는 함수를 ***콜백 함수***라고 부른다.)



콜백 함수를 전달받은 고차함수는 콜백 함수를 호출할 수 있다.

조건에 따라 콜백 함수의 실행 여부를 결정할 수도 있고, 여러번 실행할 수도 있다.



- 다른 함수를 인자로 받는 경우

  ```js
  function double(num) {
    return num * 2
  }
  
  function doubleNum(func, num) {
    return func(num)
  }
  ```

  함수 doubleNum은 다른 함수를 인자로 받는 고차 함수이다. 첫번째 인자 `func`에 함수가 들어올 경우, `func`라는 함수는 `doubleNum`의 콜백 함수가 된다.



- 함수를 리턴하는 경우

  ```js
  function adder(added) {
    return function(num){
      return num + added
    }
  }
  ```

  위 함수는 다른 함수를 리턴하는 고차 함수이다. (인자 1개를 입력받아 익명함수를 리턴)



- 함수를 인자로 받고, 함수를 리턴하는 경우

  ```js
  function double(num) {
    return num * 2;
  }
  
  function doubleAdder(added, func) {
    const doubled = func(added);
    return function (num) {
      return num + doubled;
    };
  }
  ```





### map : 배열의 각 요소가 특정 함수에 의해 다른 요소로 지정된다

```js
let num = [1, 2, 3]

let result = num.map(function(el) {
  return el * 2
})

return result;
```

map 함수는 입력받은 배열의 각 요소들을 쪼개어 내장 익명 함수에 하나씩 인자로 던져주고, 내장 익명 함수의 연산을 거쳐 새로운 배열에 결과값을 저장한다.



### filter : 배열의 각 요소를 특정 함수로 선별하여 분류한다

```js
let num = [1, 2, 3]

let result = num.filter(function(el) {
  return el % 2 !== 0
})

return result;
```

filter 함수는 입력받은 배열의 각 요소들을 쪼개어 내장 익명 함수에 하나씩 인자로 던져주고, 조건을 판별하여 true인 요소들만 새로운 배열에 결과값을 저장한다.



### reduce : 배열의 각 요소를 특정 함수에 따라 원하는 하나의 형태로 응축한다

```js
let num = [1, 2, 3]

let result = num.reduce(function(acc, cur, idx) {
  return acc + cur;
  return acc;
}, 1)

return result;
```

reduce는 흔히 *누산하는 함수*로 이해하는 경우가 많은데, 오히려 반복문과 조건문이 결합된 형태에 더 가까운 성질을 가지고 있다. 위 예시는 누산기로 사용했을 때의 코드 예시이고, 반복문과 조건문이 결합된 형태로 사용하게 되면 아래와 같이 코드를 작성할 수 있다.

```js
return newArr.reduce(function(a, b) {
  if(a.length <= b.length){
    return a;
  } else {
    return b;
  }
})
```



