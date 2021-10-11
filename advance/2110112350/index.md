---
layout: post
type: advance
date: 2021-10-11 23:50
draft: false
category: Typescript
title: 타입스크립트로 DOM 조작을 해보자
subtitle: DOM을 까먹은건 아니쥬?
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [Javascript, Typescript]
---


---



## 의미

react나 vue같은 라이브러리를 이용하여 코딩하다 보면 사실 js로 dom을 조작하는 것은 애초에 배울 필요가 없었을 수도 있겠다는 생각이 들게 된다.

그렇지만 자바스크립트가 탄생한 원래 목적이 dom 조작과 변경이기 때문에 타입스크립트에서도 dom 조작과 변경하는 방법을 알아 두기는 해야 할 것 같아서 한번 배워 보았다.





## strictNullCheck

tsconfig.json에서 null이 들어올 경우 체크해 주는 옵션을 먼저 켜 주어야 한다.

변수를 조작하기 전에 이 값이 null인지 알려주기 때문인데, 생각보다 상당히 도움이 될 수 있다고 한다.

```typescript
"strictNullChecks" : true

아니면 그냥 "strict" : true 이렇게 써둬도 strictNullChecks옵션이 자동으로 켜진다
```





## HTML 파일에서 '찾고 변경' 해보기

index.html 파일에 아래와 같은 코드가 작성되어 있다고 가정한다.

```html
<h4 id="title">Hello, world</h4>

<a id="link" href="teamddh.com">링크</a>
<button id="btn">버튼</button>

<script src="convertedts2js.js"></script>
```

script 파일을 읽어올 때에는 당연히 ts에서 js로 컴파일 된 파일을 집어넣어 주어야 한다.



### h4 제목 바꿔보기

먼저, h4 제목을 다른 글자로 변경할 때 js에서는 아래와 같이 작업한다

```js
let title = document.querySelecton('#title')
title.innerHTML = "안녕, 세상아"
```

그러나 타입스크립트에서는 오류를 반환한다.

strict 옵션 때문에 ***title이라는 변수가 null일 수 있음***이라는 오류를 알려주는데,

셀렉터로 html을 찾으면 타입이 `Element | null`이기 때문이다. (html을 못 찾을 경우 null이 됨)

이 때문에 ***type narrowing(if문)*** 또는 ***type assertion(as문법)***으로 해결해야 한다.



> **narrowing으로 해결**
>
> ```typescript
> let title = document.querySelector('#title')
> if (title != null) {
>   title.innerHTML = "안녕, 세상아"
> } else {
>   여기에도 무언가 추가해 주면 완벽해진다.
> }
> ```
>
> 



> **instanceof narrowing으로 해결**
>
> ```typescript
> let title = document.querySelector('#title')
> if (title instanceof HTMLElement) {
>   title.innerHTML = "안녕, 세상아"
> }
> ```
>
> instanceof 라는 연산자를 사용한다.



> **assertion으로 해결**
>
> ```typescript
> let title = document.querySelector('#title') as HTMLElement;
> title.innerHTML = "안녕, 세상아"
> ```
>
> 임시로 HTMLElement로 무조건 들어온다고 알려주는 방식이기 때문에 오류를 즉시 해결할 수 있지만,
>
> 언제까지나 임시방편이기 때문에 반드시 나중에 코드를 정상적으로 수정해야 한다.
>
> (이 상태로 계속 사용하는 버릇을 들인다면 타입스크립트의 장점을 깎아먹는 셈이다)



> **optional chaining 연산자로 해결**
>
> ```typescript
> let title = document. querySelector('#title');
> if (title?.innerHTML != undefined) {
>     title.innerHTML = "안녕, 세상아"
>     }
> ```
>
> title이라는 자료 안에 innerHTML이 존재하면 그 타입을 사용하고, 존재하지 않는다면 undefined로 남겨달라는 뜻이다.



### a href 속성 바꿔보기

기존 js에서는 쿼리셀렉터로 찾은 뒤 객체 속성값을 재할당 해 주면 바꿀 수 있었지만, 타입스크립트에서는 불가능하다.

```js
let link = document.querySelector('#link')
link.href = 'https://naver.com'
```

이와 같은 방법으로는 무조건 오류가 발생한다.



타입스크립트를 이용하여 작성한다면 아래처럼 생각할 수 있는데,

```typescript
let link = document.querySelector('#link')
if (link instanceof HTMLElement) {
  link.href = 'https://naver.com'
}
```

이렇게 하면 **오류가 발생한다**

왜냐면 html 태그 종류별로 정확한 타입 명칭이 모두 존재하기 때문이다.

> a 태그 : HTMLAnchorElement
>
> img 태그 : HTMLImageElement
>
> h4 태그 : HTMLHeadingElement
>
> ...
>
> 모든 태그마다 다 명칭이 존재하기 때문에 모두 외우지는 말고 자동완성을 이용하도록 하자
>
> ...
>
> 
>
> ### 근데 이게 왜 그러냐면
>
> 타입스크립트에서 쓸 수 있는 타입들은
>
> Element에 들어있는 것을 복사한 뒤 몇개 더 추가하여 HTMLElement 타입을 만들었고,
>
> HTMLElement에 들어있는 것을 복사한 뒤 몇개 더 추가하여 HTMLAnchorElement 타입을 만드는 식으로 제작되었다.
>
> 
>
> 셀렉터로 대충 찾으면 Element타입이라는게 부여가 되는데,
>
> 타입스크립트는 아직 이 태그가 정확히 어떤 것인지 추론할 수 없기 때문에 광범위한 타입을 지정하는 것이다.
>
> Element타입은 광범위한 일반 html태그의 특징을 정리해 둔 타입이기 때문에 href나 src와 같은 속성이 없다.
>
> 
>
> 반면 이후에 만들어진 HTMLAnchorElement와 같은 상세한 타입을 뜯어보면
>
> href, style, class, id와 같은 속성을 가질 수 있다고 정의되어 있다.
>
> 이 때문에 a태그에게 어울리는 타입인 HTMLAnchorElement 타입을 사용할 수 있는 지 instanceof 키워드로 확인해야 한다.
>
> 또한 타입스크립트는 이 확인 과정을 narrowing으로 인정하기 때문에 instanceof와 상세 타입 명칭을 입력하는 것으로 갈음할 수 있는 것이다.

```typescript
let link = document.querySelector('#link')
if (link instanceof HTMLAnchorElement) {
  link.href = 'https://naver.com'
}
```

이 때문에 정확하게 입력한다면 위와 같이 타입을 입력하여야 한다.





### 이벤트리스너 부착해보기

버튼 실행을 위해 이벤트리스너를 부착할 때에도 타입을 지정해야 정상적으로 작동한다.

```js
let btn = document.getElementById('btn');
btn.addEventListener('click', function(){
  console.log('버튼이 눌렸습니다')
})
```

자바스크립트로 위와 같이 작성하여 이벤트리스너를 부착하게 되는 데, 타입스크립트에서는 btn이라는 변수가 null일 수 있다는 에러를 반환한다.



타입스크립트로 narrowing하여 해결한다면 아래와 같은 코드가 될 것이다

```typescript
let btn = document.getElementById('btn');
if (link instanceof HTMLButtonElement) {
  btn.addEventListener('click', function(){
  console.log('버튼이 눌렸습니다')
})
}
```



> ### 또 다른 해결법(optional chaining)
>
> 2020년 이후에 업데이트 된 브라우저들은 모두 `?.` 연산자를 사용할 수 있다.
>
> `원본?.세부`의 형태로 볼 수 있는데, 원본 object에 세부 자료가 ***있을 경우 뽑아주고 없을 경우 undefined***로 뽑아주는 조건문과 동일하게 작동한다.
>
> 이 때문에 아래와 같이 작성해도 정상 작동한다
>
> ```typescript
> let btn = document.getElementById('btn');
> btn?.addEventListener('click', function(){
>   console.log('버튼이 눌렸습니다')
> })
> ```
>
> 



### 한번에 여러 파일 변경해보기(querySelectorAll)

```html
<a class="daum" href="daum.net">다음</a>
<a class="daum" href="daum.net">다음</a>
<a class="daum" href="daum.net">다음</a>
<a class="daum" href="daum.net">다음</a>
```

html 파일 내에 위와 같이 여러 a태그 내용을 바꾸어 주어야 한다고 가정했을 때,

아래와 같이 narrowing하게 되는데, 오류가 발생할 것이다.

```typescript
let link = document.querySelectorAll('.daum');

link.forEach((a)=> {
  if ( a instanceof HTMLAnchorElement) {
    a.href = 'kakao.com'
  }
})
```

실제로 위와 같이 `querySelectorAll`을 사용하면 많은 요소를 한번에 찾을 수 있으나,

타입이 예상과는 다르게 `NodeListOf<...>`와 같이 표시된다.

많은 요소를 한번에 찾게 되면 이러한 타입으로 표시되어 버리는 데 이유는 아직 잘 모르겠으나, 정상적으로 작동하지 않기 때문에 아래와 같이 코드를 변형하여 사용해야 정상적으로 의도한 내용을 실행할 수 있다.

(또한 forEach도 정상 작동이 안 된다고 한다 - 나중에 실험해 볼 예정)



```typescript
let link = document.querySelectorAll('.daum')

for (let i = 0; i < 4; i++) {
  let a = link[i];
  if(a instanceof HTMLAnchorElement){
    a.href = 'kakao.com'
  }
}
```

일반 for문을 이용할 경우 변수를 만들어 주어야 매끄럽게 narrowing이 가능하다.

