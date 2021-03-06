---
layout: post
type: UX
date: 2021-10-26 19:20
draft: false
category: HTML
title: 시멘틱 마크업, 블록&인라인
subtitle: Plain Old Semantic HTML
writer: 000000
post-header: true
header-img : img/about.jpeg
hash-tag: [HTML, POSH, Semantic Markup]
---

---



## 시멘틱 마크업

시멘틱 마크업은 POSH(Plain Old Semantic Html)로 불리는데,

단어 그대로 ***평범하고 오래된 의미론적인 HTML***이라는 뜻이다.

즉, 기계나 컴퓨터가 잘 이해할 수 있도록 하는 것을 뜻한다



### How to markup

브라우저나 컴퓨터가 가장 잘 이해할 수 있도록 만들 때 중요한 것은 아래와 같다.

- 의미에 맞는 태그나 요소 사용
- 문서 표현 시 구조화

```html
<b>굵은</b> vs <strong>중요한</strong>
<i>기울어진</i> vs <em>강조하는</em>
<u>밑줄친</u> vs <ins>새롭게 추가된</ins>
<s>중간선이 있는</s> vs <del>삭제된</del>
```

위와 같이 태그를 사용하여 작성하게 되면, 좌-우 요소가 같은 모습으로 표현되지만 의미가 같지는 않다.

이 때문에 필요에 따라 적절하게 사용하는 것이 중요하다.



HTML5에서 새로 생긴 시멘틱 요소는 아래와 같다.

- `article` : 본문의 주 내용이 들어감
- `aside` : 주 내용과 간접적으로 연관된 표현 (주석)
- `figcaption` : figure 내 콘텐츠에 대한 설명 또는 범례
- `figure` : 독립적인 콘텐츠를 표현
- `footer` : 꼬릿말(구획의 작성 정보나 관련 문서 등)
- `header` : 머릿말(소개 및 탐색을 위한 제목)
- `main` : 본문, 주 콘텐츠
- `mark` : 현재 맥락에 관련이 깊거나 중요한 부분 하이라이트
- `nav` : 문서의 부분 중 현재 페이지 내 또는 다른 페이지로의 링크를 보여주는 구문 생성(`li`태그 활용)
- `section` : 내용을 내부에서 구획화
- `time` : 시간의 특정 지점 또는 구간 표현. datetime라는 특성으로 유효한 날짜 구문 마크업 가능





## 블록&인라인

### 블록 레벨 요소

부모 요소의 가로 영역에 맞게 꽉 채워져 표현되는 요소.(div로 이해하면 편함)

양 옆으로 다른 요소가 배치되지 않게 박스를 생성하며, 박스의 위아래로 줄바꿈이 발생한다.

블록 레벨 요소는 일반적인 모든 요소(블록, 인라인 레벨 등)를 포함할 수 있다.

> 예외 : `h1~h6`, `<p>` 는 블록 레벨 요소지만, 내부 요소로 Phrasing Content만 허용한다.

### 인라인 레벨 요소

하나의 라인 안에서 자신의 내용만큼의 박스를 만드는 요소. (span으로 이해하면 편함)

라인의 흐름을 끊지 않고 요소 앞뒤로도 줄바꿈이 되지 않아 다른 인라인 요소들이 자리할 수 있다.

인라인 레벨 요소는 자손으로 블록 레벨 요소를 가질 수 없다. (인라인 레벨 요소 자체가 블록 자식으로 분류됨)

> 예외 :  HTML5부터 `<a>`는 인라인 레벨 요소지만 자손으로 블록 레벨 요소를 가질 수 있다.
