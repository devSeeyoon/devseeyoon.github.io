---
layout: post
type: advance
date: 2021-10-08 16:53
draft: false
category: Typescript
title: Generic
subtitle: 타입 정보의 동적 결정
writer: 000000
post-header: true
header-img : img/about.png
hash-tag: [Javascript, Typescript]
---
> 이 포스팅의 내용은 [동료 개발자](https://kim-link.github.io)가 라이브 세션을 진행하며 정리하였고, 해당 내용을 공부하며 일부 변형하여 작성하였습니다.


---

### 제네릭의 존재 이유

제네릭은 타입 정보를 동적으로 결정하는 것을 말한다.

타입스크립트 코드를 작성할 때 타입만 다른데 함수를 한번 더 작성해야 하는 경우가 발생한다.

이와 같은 상황이 발생하면 코딩 자체도 귀찮을 뿐더러, 전체 코드의 양이 불필요하게 길어지기 때문에 메모리 최적화 면에서도 불리하게 작용할 수 있다.

이 때문에 제네릭을 이용하여 중복하여 코드를 작성하는 행위를 최소화 할 수 있다.

```typescript
function numArr(x :number, size :number) :number[] {
  let arr :number[] = [];
  for(let i = 0; i < size, i++){
    arr.push(x)
  }
  return arr;
}

function strArr(x :string, size :number) :string[] {
  let arr :string[] = [];
  for(let i = 0; i < size, i++){
    arr.push(x)
  }
  return arr;
}

let arr1 = numArr(1, 10);
let arr2 = strArr('empty', 10);
```

위 예제를 보면 `numArr` 함수와 `strArr`함수는 같은 기능을 하고 있으나 타입만 다른 형태이다.

이럴 때에는 아래와 같이 **함수 오버로드**를 사용해 주면 해결이 가능하다.



### 함수 오버로드

```typescript
function newArr(x :number, size :number) :number[];
function newArr(x :string, size :number) :string[];
function newArr(x :boolean, size :number) :boolean[];

function newArr(x :number | string | boolean, size : number) :Array<number | string | boolean> {
  let arr :Array<number | string | boolean> = [];
  for(let i = 0; i < size; i++) {
    arr.push(x);
  }
  return arr;
}

let arr1 = newArr(1, 10);
let arr2 = newArr('empty', 10)
```

첫번째 예시와 다르게 위 예시에서는 유사한 함수의 중복이 사라졌다.

입력값을 number, string, boolean 중에서 자동으로 인식하여 함수를 실행시키고 리턴값을 만들어 주는 함수가 완성된 것이다.

그러나 문제점이 아직 남아있는데, 타입을 추가하고 싶을 때에는 코드에 타입을 추가로 기입해야 하고, 함수가 다루는 타입이 늘어나게 될 수록 번거로울 뿐더러 코드의 가독성도 떨어지게 된다.

이럴 때 제네릭을 사용하게 되면 간단히 해결이 가능하다.



### 제네릭

```typescript
function newArr<T>(x :T, size :number): T[] {
  let arr :T[] = [];
  for(let i = 0; i < size; i++){
    arr.push(x);
  }
  return arr;
}

let arr1 = newArr<number>(1, 10);
let arr2 = newArr<string>('empty', 10)
```

제네릭은 함수 이름 우측에 `<>`를 이용하여 입력할 수 있다. (T라고 쓴건 편의상. 원하는 이름으로 할 수 있음)

타입은 나중에 동적으로 결정 될 것이며, 제네릭 타입은 **매개변수와 구현 모두 사용 가능**하다.

예시의 arr1, arr2처럼 타입을 명시하여 이용할 수도 있으나, 타입을 적지 않아도 자동으로 추론하여 작동할 수도 있다.





### extends

타입스크립트에서 제네릭을 사용할 때에는 입력 가능한 값의 제한이 없다.

반면, 리액트와 같은 라이브러리나 api는 입력 가능한 값의 범위를 제한한다. (ex. 리액트의 속성은 객체만 허용)

이를 위해 제네릭은 타입의 종류를 제한할 수 있는 기능을 제공하는데, 이것이 바로 extends이다.

```typescript
function greeting<T extends number | string>(x :T) :T {
  return 'hello agent' + ' ' + x;
}

greeting(1); // hello agent 1
greeting('vanessa'); // hello agent vanessa
greeting([]); // error
```

위 예시 코드에서는 T의 타입이 number 또는 string이라고 정의를 하였다.

제네릭에서의 extends는 **`A extends B` => A가 B에 할당 가능해야 한다** 로 이해하면 쉽다.

예시 코드에서 `T extends number | string`이라고 적힌 것은, **T가 number 또는 string에 할당 가능해야 함** 으로 볼 수 있고, 따라서 배열을 입력하였을 때 에러가 발생하는 것을 확인할 수 있다.



```typescript
interface Person {
  name : string;
  age : number;
}

interface Korean extends Person {
  knowbts : boolean;
}

type T1 = keyof Person;

function swap<T extends Person, K extends keyof Person>(p1 :T, p2 :T, key :K) :void {
  const temp = p1[key];
  p1[key] = p2[key];
  p2[key] = temp;
}

const p1 :Korean = {
  name : '엄준식',
  age : 25,
  knowbts : true,
}

const p2 :Korean = {
  name : '김포도',
  age : 17,
  knowbts : false,
}

swap(p1, p2, 'age');
```

위 예시를 보면 `Korean`은 `Person`을 확장하여 타입을 정의하였다.

`swap` 함수에서 `Person`을 확장하여 `T`를 정의하였고,

`keyof Person`을 확장하여 `K`를 정의하였다.

**`keyof`라는 것은 keyof 우측에 작성된 인터페이스의 모든 속성 이름을 나열한 것이다.**

위 예시 코드에서 `swap`함수가 하는 역할은, 두 개의 객체와 하나의 Key를 입력받아 Key에 해당하는 값을 서로 맞바꾸는 것임을 알 수 있다.



