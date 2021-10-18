---
layout: post
type: advance
date: 2021-10-14 23:25
draft: false
category: Typescript
title: never타입은 무엇인가
subtitle: 그건 지금부터 알아봐야함
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [Javascript, Typescript]

---


---



### Never

이 타입은 ***함수에 붙이는 return type***으로 사용할 수 있다.

```typescript
function test() :never {
  
}
```



단, 조건이 있어야 한다

- 절대 return을 하지 않아야 하고
- 함수 실행이 끝나지 않아야 한다(endpoint가 없어야 함)



위 2가지 조건은 사실 같은 이야기인데, 모든 자바스크립트 함수 최하단엔 return undefined라는 숨겨진 코드가 있기 때문에 위와 같이 조건을 설명해야 맞다.



endpoint가 없어야 한다는 조건을 충족하지 못하는 경우는 아래와 같다

```typescript
function test() {
  console.log(123)
}
```

우리 눈에는 함수가 하는 일이 없고, 리턴하는 것도 없어 보이지만

실제로는 함수 내부 코드 실행이 콘솔 찍은 뒤 종료되기 때문에 2번째 조건을 충족하지 못한다





```typescript
function test() :never {
  while(true) {
    console.log(123)
  }
}
```

위와 같은 함수에는, while문이 종료되지 않고 계속해서 내부 코드를 실행하기 때문에(무한히 실행) never타입을 지정할 수 있다.





```typescript
function test() :never {
  throw new Error('msg : error')
}
```

여기서는 강제로 에러를 발생시키면 전체 코드 실행이 중단되기 때문에 2가지 조건을 모두 충족하여 사용할 수 있다.

***코드 실행이 중단되는것과 끝나는 것의 차이를 유념해야 한다***







위 내용을 보면, 2가지 조건을 모두 충족하는 함수를 만들 일이 거의 없기 때문에 never타입은 사용할 일이 거의 없다.

무언가를 return하지 않을 경우 void 타입을 사용하면 되고, never은 코드를 잘못 작성했을 때 등장하는 타입이라고 생각하면 된다.



### never 타입이 등장하는 경우

- 파라미터가 never타입이 되는 경우

  ```typescript
  function test (x :string) {
    if( typeof x === "string"){
      x + 1
    } else {
      x
    }
  }
  ```

  위 함수는 narrowing을 잘못 사용한 함수이다. 이 때 파라미터의 타입은 never가 된다.



- 자동으로 never타입을 가지는 경우

  ```js
  자바스크립트는 함수를 만드는 방법이 2가지가 있다
  
  function test() {
    throw new Error()
  }
  
  let test2 = function() {
    throw new Error()
  }
  ```

  함수 선언식에서 아무것도 return하지 않고 끝나지도 않을 경우 void 타입이 자동으로 return타입으로 할당되며, 함수 표현식이 아무것도 return하지 않고 끝나지도 않을 경우 never타입이 자동으로 return타입으로 할당된다.

  또는 tsconfig.json에서 strict 옵션을 켤 경우 any타입을 함부로 지정하지 않는 경우가 있는데, 배열같은 것을 타입 지정 없이 대충 만들면 원래는 any[]와 같은 타입이 지정되어야 하나, any를 쓸 수 없어서 never[]로 지정되기도 한다