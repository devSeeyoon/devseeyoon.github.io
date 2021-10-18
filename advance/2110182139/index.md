---
layout: post
type: advance
date: 2021-10-14 23:25
draft: false
category: Typescript
title: interface
subtitle: type와 다른 방식
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [Javascript, Typescript]

---


---



### Interface

interface 문법을 쓰면 object의 타입을 보다 편리하게 지정할 수 있다.

```typescript
interface Objtype {
  color :string,
    width :number,
}
    
let Circle :Objtype = { color : 'red', width : 100}
```

interface는 객체의 형태 그대로 작성하면 된다.

또한 type alias와 용도와 기능이 똑같다. (***대문자로 작명***하고 `{}`안에 타입을 지정해주면 된다)





### extends

interface의 장점은 extends도 가능하다.



```typescript
interface Student {
  name :string,
}

interface Teacher extends Student {
  age :number,
}
```

위와 같은 코드를 작성했을 때, student 타입은 name 속성을, teacher 타입은 name과 age 속성을 가지고 있게 된다.





### type과의 차이점 1 : extends 문법

type alias와 interface는 거의 같은 기능을 제공한다.

우리가 공부한 내용에서 느낄 수 있는 차이점은 extends 문법이 약간 다른 정도이다



- interface의 경우

```typescript
interface Animal {
  name :string
}

interface Cat extends Animal {
  legs :number
}
```



- type alias의 경우 (interface도 `&`기호를 이용해 복사가 가능하다)

```typescript
type Animal {
	name :string
}

type Cat = Animal & { legs :number}
```



### type과의 차이점 2 : 타입 이름 중복 선언

interface의 경우 타입 이름 중복 선언을 허용하며, 중복 시 extends와 동일하게 동작한다.

type의 경우에는 중복 선언을 허용하지 않는다.



이러한 차이 때문에 일반적인 상황에서는 type 키워드로 엄격하게 관리하는 것이 좋으나, 여러 사람이 코드를 이용하는 상황이 많으면 interface로 유연하게 만들어 두는 것도 고려해 볼 수 있다.



