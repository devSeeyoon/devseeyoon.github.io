---
layout: post
type: UX
date: 2021-10-26 19:02
draft: false
category: HTML
title: Contents Model
subtitle: 
writer: 000000
post-header: true
header-img : img/about.jpg
hash-tag: [HTML, Contents Model, Metadata, Flow, Sectioning, Heading, Phrasing, Embedded, Interactive]
---



> HTML5에는 요소들이 가지고 있는 성격에 따라 요소의 종류를 정의하는 규칙들이 있다.
>
> 요소는 이 규칙들을 준수해야 하며, 반드시 HTML 권고안을 따라야 한다.
>
> 이러한 규칙에 대해 비슷한 성격의 요소들끼리 그룹화한 것이 콘텐츠 모델이며,
>
> 각각의 요소들은 하나 또는 여러개의 콘텐츠 모델에 속하게 된다

---

### Metadata

콘텐츠의 style, script를 설정하거나 다른 문서와의 관계 등의 정보를 포함하는 요소

- base
- link
- meta
- noscript
- style
- title

대부분 head 태그 내에 삽입된다는 것이 특징이다.



### Flow

문서의 자연스러운 흐름에 의해 배치되는 요소.

metadata에 해당하는 일부 태그를 제외한 대부분의 요소가 flow에 포함된다

```text
a, abbr, address, map>area, article, aside, audio, b, bdo, blockquote, br, button,
canvas, cite, code, datalist, del, details, dfn, div, dl, em, embed,
fieldset, figure, footer, form, h1 ~ h6, header, hgroup, hr, i, iframe, img,
 input, ins, kbd, keygen, label, map, mark, math, menu, meter, nav, noscript, object, ol,
output, p, pre, progress, q, ruby, samp, script, section, select, small, span, strong,
style[scoped], sub, sup, svg, table, textarea, time, ul, var, video, wbr
```



### Sectioning

문서의 구조와 관련된 요소.

- article
- aside
- nav
- section

문서 자체의 구조나 아웃라인에 영향을 주며, HTML5에서 새로 생긴 것들이다



### Heading

각 section의 header를 정의하는 heading 태그

- h1 ~ h6



### Phrasing

문서의 텍스트, 텍스트를 꾸며주는 문단 내부 레벨로 사용되는 요소

```text
a, abbr, map>area, audio, b, bdo, br, button, canvas, cite, code, datalist, del, dfn, em, embed,
 i, iframe, img, input, ins, kbd, keygen, label, map, mark, math, meter, noscript, object, output,
 progress, q, ruby, samp, script, select, small, span, strong, sub, sup, svg, textarea, time,
var, video, wbr
```



### Embedded

외부 콘텐츠를 표현하는 요소들이 포함되며, 오디오나 비디오 또는 이미지 등 멀티미디어 관련 요소가 해당한다.

- audio
- canvas
- embed
- iframe
- img
- math
- object
- svg
- video



### Interactive

사용자와 상호작용을 하는 요소. 대표적으로 form이 해당한다.

- a
- audio[controls]
- button
- details
- embed
- iframe
- img[usemap]
- input
- keygen
- label
- menu
- object[usemap]
- select
- textarea
- video[controls]

