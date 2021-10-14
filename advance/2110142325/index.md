---
layout: post
type: advance
date: 2021-10-14 23:25
draft: false
category: Typescript
title: type alias
subtitle: 를 함수와 메소드에 지정해보자
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [Javascript, Typescript]

---


---





### 함수에 지정해보자



함수에 들어갈 타입들도 type키워드를 이용해 저장해서 쓸 수 있다.

```typescript
type tester = (x :number, y:number) => number;
```



함수를 만들 때 사용해야 하는데, 중요한 건

`function 함수명 :tester (){}` 이런 형식으로는 사용이 불가하다.

-> `function`키워드는 `()` 내부와 오른쪽에만 타입 지정이 가능하기 때문.

이 때문에 함수를 만들 때 `let 함수명 = function(){}`의 형식(`함수명:타입별명`)과 같이 지정해서 사용해야 한다.



```typescript
type tester = (x :number, y :number) => number;

let yee :tester = function(x, y) {
  return x + y;
}
```





### 메소드에 지정해보자

객체 안에 있는 함수에도 type 키워드를 이용해 저장해서 쓸 수 있다.



아래와 같은 객체가 있다고 가정했을 때

```typescript
let codestates = {
  boss : 'ingi kim',
  SEB : 28,
  plusOne (x){
    return x + 1;
  },
  changeName : () => {
    console.log('hello')
  }
}

codestates.plusOne(1);
codestates.changeName();
```



plusOne이라는 함수는 숫자를 넣어서 숫자를 리턴해야 하고,

changeName이라는 함수는 아무것도 리턴하지 않는다.



위 조건을 만족하기 위해서는 아래와 같이 코드가 작성되어야 할 것이다.

```typescript
type info = {
  boss : string,
  SEB : number,
  plusOne : (x :number) => number,
  changeName : () => void
}

let codestates :info = {
  boss : 'ingi kim',
  SEB : 28,
  plusOne (x) {
    return x + 1;
  },
  changeName : () => {
    console.log('hello')
  }
}
```

