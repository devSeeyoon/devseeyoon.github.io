---
layout: post
type: vue
date: 2021-10-26 19:00
draft: false
category: Vue.js
title: 리액트 vs Vue
subtitle: 다들 리액트를 배워놓고 vue를 쓰는 이유는 뭘까?
writer: 000000
post-header: true
header-img : img/about.jpeg
hash-tag: [Vue.js]
---



---



# Vue

카카오테크를 읽어보면 FE개발자들이 사용하는 프레임워크는 React와 Vue.js이며,

React를 사용하는 업무가 아주 근소하게 많다고 한다.

네이버에서도 새로운 페이지를 만들때 React를 이용하지 않고 Vue를 이용해서 만드는 경우가 많다.



### Vue를 이용하는 이유

***쉬워서***라고 한다.

React, Angular, Vue 모두 똑같이 web-app을 만들어 낼 수 있지만,

Angular는 매우 방대하며 Typescript를 강제로 사용해야 하고,

React는 기존 Javascript 문법을 매우 많이 활용하고

Vue는 vue 문법을 새로 배워야 한다.



그래서 Javascript에 능숙하지 않아도 간단한 vue 문법만 잘 공부하면

초보도 2~3시간이면 웹앱을 만들어 낼 수 있다고 한다.



쉽다는 것의 예시를 조금 더 디테일하게 하자면

```react
const printpage = () => {
  if (true) {
    return <p>this</p>
  } else {
    return <p>not this</p>
  }
  
  return (
  	<div>{printpage()}</div>
  )
}
```

React에서는 위와 같은 형식으로 if문을 작성하는데, vue에서는 아래와 같다고 한다

```vue
<template>
	<div>
    <p v-if="show">this</p>
    <p v-else>not this</p>
  </div>
</template>
```





그리고 리액트에서는 아래와 같이 state를 변경하지만

```react
const [human, setHuman] = React.useState(['Kim', 18, 'Female'])

let humanCopy = [...human];
humanCopy[0] = 'Lee';
setHuman(humanCopy);
```

vue에서는 아래와 같이 편리하게 바꿀 수 있다

```vue
return {
	human: ['Kim', '18', 'Female']
}

this.human[0] = 'Lee';
```





반복문 또한 큰 차이를 보인다

```react
function List() {
  const todos = ['eat', 'sleep', 'work']
  return (
    <ul>
      {
        todos.map((todo)=>
                 <li key={todo}>{todo}</li>)
      }
    </ul>
  )
}

export default List
```

```vue
<template>
	<ul>
    <li v-for="todo in todos" :key="todo">{{todo}}</li>
  </ul>
</template>

<script>
	export default {
    data()
    return {
      todos: ['eat', 'sleep', 'work']
    }
  }
</script>
```



같은 기능을 구현한다고 했을 때 대부분 vue가 코드가 더 간결하고 직관적이며,

HTML 구조와 유사하기 때문에 페이지에 대한 구조 파악 또한 쉽다.



또한, React는 코드를 작성하는 방법이 매우 자유로워 프로그래밍 언어를 적극 활용하여 개발하게 되지만

vue는 무조건 답과 방법이 정해져 있다.

시니어 개발자가 되어 자유롭게 언어들을 활용하며 개발할 수 있다면 단점이 될 수는 있으나,

코드 작성이 익숙치 않은 주니어 개발자에게는 엄청난 장점이 될 수 있으며,

여러 사람이 협업하게 될 때 코딩 스타일이 각기 다르면 코드 리뷰 시 작동 흐름을 파악하는 데에만 상당한 시간을 소요하게 되는데 vue는 대부분 비슷하기 때문에 불필요한 태스크를 줄일 수 있다.





