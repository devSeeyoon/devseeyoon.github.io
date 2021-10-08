---
layout: post
type: advance
date: 2021-10-08 16:53
draft: false
category: Typescript
title: 함수 rest 파라미터
subtitle: 그리고 destructuring 할 때 타입 지정하기
writer: 000000
post-header: true
header-img : img/about.png
hash-tag: [Javascript, Typescript]
---


---



### rest parameter가 뭐더라?

```js
function test(...a) {
  
}
```

파라미터가 몇개가 들어올 지 모를때 쓰는 방법. 다른 파라미터 뒤에 붙여서 써야 한다



### spread operator과 헷갈리면 안됩니다

```js
let arr = [1, 2, 3];
let arr2 = [4, 5];
let arr3 = [...arr, ...arr2]
```

이렇게 쓰는 spread operator는 **괄호를 벗겨주세요**라는 명령어로 생각해야 한다.

이건 rest parameter와 다르기 때문에 혼동하면 안된다



---

### 타입 지정하는 방법

rest 파라미터 또한 타입 지정이 필요하다. 타입 지정이 되지 않는다면 `any` 상태로 추론하게 되어 각종 오류가 발생할 수 있다.

```typescript
function test(...a :number[]){
  
}
```

그렇기 때문에 위와 같이 타입을 지정해 줄 수 있는데, 주의할 점은 **rest파라미터는 항상 배열에 값을 담아오기 때문에 배열로 타입 지정을 해 주어야 한다**.

만약, rest parameter에 number, string, boolean이 모두 포함되어 있다면 `type` 키워드를 이용해 사전에 변수처럼 타입을 선언해 놓은 뒤 파라미터에서 타입을 지정하면 될 것이다.



### destructuring

디스트럭처링은 배열 내의 여러 값을 빼내어 사용할 때 불필요한 코드를 줄여 주는 것을 말한다.

```js
let arr = [1, 2, 3, 4, 5]

let idx0 = arr[0]
let idx1 = arr[1]
let idx2 = arr[2]
```

배열의 각 인덱스를 빼내어 사용하려면 위와 같은 작업을 통해 각 변수마다 할당을 해 주어야 하는 일이 있었다.

그러나 디스트럭쳐링을 이용하면 아래와 같이 한번에 원하는 만큼 빼내어 사용할 수 있다.

```typescript
let [idx0, idx2, idx2] = [1, 2, 3]

let { student : student, age : age } = {student : true, age : 20}
let { student, age } = { student : true, age : 20 }
// 자바스크립트 문법에 따라 윗줄처럼 양측 이름이 동일한 상황이라면 아랫줄처럼 생략이 가능하다
```



### 함수 파라미터에 destructuring 가능

기존에 함수 파라미터에 객체를 넣으려면 아래와 같은 방법으로 넣어야 했다

```js
let obj = { student : true, age : 13 }

function test(a, b) {
  console.log(a, b)
}

test(obj.a, obj.b)
```



하지만 이러한 방법 대신 디스트럭처링을 이용하면 편리하게 객체의 변수명만 삽입하여 처리할 수 있다.

```typescript
let obj = { student : true, age : 13 }

function test({student, age}) {
  console.log(student, age)
}

test(obj)
```



여기서 이제 함수 파라미터에 타입을 지정해야 한다.

```typescript
let obj = { student : true, age : 13 }

function test({student, age} :{student :boolean, age :number}){
  console.log(student,age)
}

test(obj);
```

위와 같이 타입을 지정할 수 있고, 타입으로 인해 코드가 길어지거나 보기 불편해진다면 `type`키워드를 이용하여 간소화 할 수 있다.