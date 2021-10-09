---
layout: post
type: advance
date: 2021-10-09 21:26
draft: false
category: Typescript
title: Readonly, type extend
subtitle: 읽기 전용, 타입 합치기
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [Javascript, Typescript]
---


---



### readonly

자바스크립트에서 변경되지 않아야 하는 변수라면 `const`를 사용하여 선언하기 마련이다.

그런데, 알고보면 `const`는 재할당을 금지하는 변수이기 때문에 `const`로 선언한 변수의 내용이 **객체**라면 객체 내부의 값 수정은 자유롭게 가능한 상태가 된다.

```js
const bts = { company : "bighitEnt"}

bts.company = "hive"
```

위 예시처럼 객체 수정이 자유롭게 가능하기 때문에 데이터를 확실하게 보존하지 못하는 취약점이 발생한다.



반면 타입스크립트에서는 object 자료 수정도 막을 수는 있으나, ts파일에서만 적용되고 js로 컴파일되면 다시 자바스크립트처럼 자료 수정이 가능하다는 점은 염두에 두고 코딩을 해야 할 것이다.



```typescript
type btsinfo = { readonly company : string }

const bts :btsinfo = {
  company : 'hive'
}

bts.company = 'cube' // error
```

이와 같이 `type`키워드를 이용하여 타입을 지정할 때 `readonly` 옵션을 같이 써주게 되면 const로 선언한 뒤 변경하려고 할 때 오류를 내뱉으며 재할당 및 변경을 거부한다.



다시 한 번 명심할 것은,

> #### readonly는 컴파일 시 에러를 내는 것일 뿐, 변환된 js파일로는 기존 자바스크립트 문법대로 작동한다



### type

`type` 키워드는 타입들을 변수화하여 사용할 수 있는 키워드라고 이미 배워서 알 고 있는 내용이다.

근데 이걸 조금 더 유연하게 사용할 수 있다. **type 키워드 여러개를 합칠 수도 있는 것**

```typescript
type nametype = string;
type agetype = number;
type newType = nametype | agetype
```

위와 같이 OR연산자를 이용하여 Union type을 만들 수도 있다.

또한, object에 지정한 타입의 경우에도 합칠 수 있다

```typescript
type typeX = { x :number };
type typeY = { y :number };
type XY = typeX & typeY // { x :number, y :number}
```

object에 지정된 타입은 `&`를 이용하여 속성을 합칠 수 있다 (extend 한다고 함)

그리고 반드시 위 예시처럼 type alias & type alias만 가능한 것이 아니라, `type alias & { name :string }`과 같은 extend도 가능하다.



> ### 💡 `type` 키워드는 재정의가 불가능하다
>
> ```typescript
> type songtype = string;
> type songtype = boolean;
> ```
>
> 위와 같이 한번 선언한 type을 재정의(재할당)하려고 하면 오류가 발생한다.
>
> 이렇게 재정의가 필요할 때는 `interface`키워드를 이용하면 가능하다.
>
> 하지만, interface로 재정의를 하거나 `&`하게 되면 엄격한 타입스크립트의 장점을 반감시키는 것이므로 주의가 필요하다.

