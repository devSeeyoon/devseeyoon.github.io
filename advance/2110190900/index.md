---
layout: post
type: advance
date: 2021-10-19 09:00
draft: false
category: Typescript
title: Public, Private
subtitle: 은근히 중요합니다
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [Javascript, Typescript]

---


---



### Public

class안에서 `public` 키워드를 사용할 수 있다.

원하는 속성의 왼쪽에 붙여두면 어디서든 사용할 수 있다.

```typescript
class User {
  public name :string;
  
  constructor(){
    this.name = 'kim';
  }
}

let user1 = new User();
user1.name = 'namjun'
```

public 키워드를 굳이 붙이지 않아도 기본적으로 public인 상태임을 유념할 것.

class 내의 prototype 함수에도 사용이 가능하다.



### Private

`private`키워드를 붙이면 수정이 불가능해진다. (무조건 class{} 중괄호 안에서만 수정 및 사용 가능)

class로부터 생산된 자식 객체에서도 사용할 수 없다. (class 중괄호 내부가 아니기 때문)

```typescript
class User {
  public name :string;
  private familyName :string;
  
  constructor() {
    this.name = 'namjun';
    let hello = 'hello' + ' ' + this.familyName; // 'hello kim'
  }
}

let user1 = new User();
user1.name = 'jangwoo' // 'jangwoo'
user1.familyName = 'Jo' // error
```

위 예시처럼 속성을 외부에서 숨기고 싶을 때 `private` 키워드를 이용한다.

바닐라 자바스크립트에서도 속성 옆에 `#`을 붙이면 private 속성이 된다

class 내의 함수에도 `private` 키워드를 붙일 수 있다.



> **Private 부여된 속성을 class 밖에서 수정해야 할 경우**
>
> private 속성을 수정하는 함수를 class 안에 만들어서 함수를 실행시키면 된다.
>
> 위 private 예제를 바탕으로 코드를 작성하면 아래와 같다
>
> ```typescript
> class User {
>   public name :string;
>   private familyName :string;
>   
>   constructor() {
>     this.name = 'namjun';
>     let hello = 'hello' + ' ' + this.familyName; // 'hello kim'
>   }
>   changeFamilyName(x :string) {
>     this.familyName = x
>   }
> }
> ```
>
> 



### 사용처

외부에서 실수로 수정하거나 변형하지 않아야 하는 속성에 `private` 키워드를 붙여 사용할 수 있다.

`private` 키워드가 붙은 속성을 수정하려면 별도의 함수를 만들어 수정해야 하기 때문에 약간의 안전장치가 더해진 것이라고 봐도 무방하다.

개발 자체에는 조금 더 시간을 소요해야 하지만 버그를 예방해주는 키워드이며, redux에서 자주 볼 수 있는 패턴이기도 하다.







### 트윅

public 키워드를 사용하면 constructor 내부에서 `this.name = name`과 같은 코드를 생략할 수 있다

```typescript
class Person {
  name;
  constructor ( name :string ){
    this.name = name;
  }
}

let human1 = new Person('tess')
```

기존에는 위와 같이 작성했다면,



```typescript
class Person {
  constructor ( public name :string){
    
  }
}

let human1 = new Person('vanessa')
```

이렇게 사용할 수도 있다.



