---
layout: post
type: advance
date: 2021-10-08 16:12
draft: false
category: Typescript
title: 타입스크립트 컴파일 세부설정
subtitle: tsconfig를 잘 써야 멍청이가 되지 않습니다
writer: 000000
post-header: true
header-img : img/about.jpeg
hash-tag: [Javascript, Typescript]
---



---

### tsconfig.json

타입스크립트를 세부 설정할 필요가 있을 때에는 `tsconfig.json`파일을 생성하거나 수정하여야 한다.

여기에는 ts파일들을 js파일로 변환할 때 어떻게 변환할 것인지 세부 설정이 가능하다.

리액트나 뷰로 프로젝트를 생성했다면 자동으로 생성되기도 한다.



```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
    	  "noImplicitAny": true,
        "strictNullChecks": true
    }
}
```

- target : 타입스크립트를 어떤 버전의 자바스크립트로 컴파일 할 지 지정할 수 있다. es2016, esnext와 같이 최신버전 문법을 입력할 수도 있다.



- module : 자바스크립트 파일 간 import 문법을 구현할 때 어떤 문법을 사용할 지 지정할 수 있다. commonjs는 require를 사용하고, es2015, esnext는 import 문법을 사용한다.



- MSIE 호환을 위해서는 위 예시처럼 es5, commonjs를 이용해야 어느정도 오류 없이 호환이 가능하나, bigint타입이나 `BigInt()` 함수와 같이 신버전에서만 표현 가능한 문법들이 있는데, 이러한 것들은 esnext 등으로 버전을 올려 주어야 사용이 가능하다.



- noImplicitAny : any타입이 의도치 않게 발생할 경우 에러메세지를 표시한다 (보통 추론의 경우)



- strictNullChecks : null이나 undefined 타입에 무언가 조작을 가하면 에러메세지를 표시한다.



### 다른 사용 가능한 옵션

tsconfig.json은 상당히 많은 컴파일러 옵션을 지정할 수 있는데, 그나마 쓰일 가능성이 있는 옵션들은 아래와 같다.

```json
{
 "compilerOptions": {

  "target": "es5",
  "module": "commonjs",
  "allowJs": true, // js 파일 ts에서 import 가능 여부 
  "checkJs": true, // 일반 js 파일에서도 에러 체크 여부 
  "jsx": "preserve", // tsx => jsx 컴파일 방법 'preserve', 'react-native', 'react'
  "declaration": true, // 컴파일시 .d.ts 파일도 자동 생성 (현재쓰는 모든 타입이 정의된 파일)
  "outFile": "./", // 모든 ts파일을 js파일 하나로 컴파일 (module이 none, amd, system일 때만 가능)
  "outDir": "./", // js파일 아웃풋 경로변경
  "rootDir": "./", // 루트 경로 변경 (js 파일 아웃풋 경로에 영향 있음)
  "removeComments": true, // 컴파일 시 주석 제거 
  "strict": true, // strict 관련, noimplicit 관련 모드 전부 켜기
  "noImplicitAny": true, // any타입 금지 여부
  "strictNullChecks": true, // null, undefined 타입 조작 시 에러메세지 
  "strictFunctionTypes": true, // 엄격한 함수 파라미터 타입 체크
  "strictPropertyInitialization": true, // 엄격한 class constructor 타입 체크
  "noImplicitThis": true, // this 키워드가 any 타입일 경우 에러메세지
  "alwaysStrict": true, // 자바스크립트 "use strict" 모드 켜기
  "noUnusedLocals": true, // 미사용 지역변수 발견 시 에러메세지
  "noUnusedParameters": true, // 미사용 파라미터 발견 시 에러메세지
  "noImplicitReturns": true, // return이 없는 함수 발견 시 에러메세지
  "noFallthroughCasesInSwitch": true, // switch문 이상하면 에러메세지 
 }
}
```

