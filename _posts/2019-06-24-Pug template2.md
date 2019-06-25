---
layout: post
title: '[NodeJS] Pug Template2'
author: HyeGyeong
categories: [Express, NodeJS]
image: 'assets/images/pug.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## Pug Template 2

#### Layouts

- html을 사용하면서 불편한 점은 header, footer 등 반복되는 부분을 복사-붙여넣기 등으로 계속 써야한다는 건데, pug를 이용하면 반복되는 부분을 따로 빼서 include 시킬 수 있다. 함수처럼 한 번 정의해두면 여러 곳에서 불러서 사용할 수 있어서 관리가 수월하다.
- ![image](https://user-images.githubusercontent.com/25483027/59974163-bc40f800-95e3-11e9-9b5b-5c245243e2a9.png)
- 모든 페이지는 header, footer, HTML head, HTML body, css link 등을 필요로 한다. views/layouts의 main은 필요한 html 요소들을 가지고 있는 기본 틀이 되는 파일이다.

```pug
//- main.pug
doctype html
html
  head
    title Pug Template
  body
    header
      h1 Pug는 쉬워요!
    main
      //- 각각 페이지의 내용이 들어갈 부분
      block content
    footer
      span &copy; footer
```

```pug
//- index.pug
extends layouts/main

block content
  p This is Index!
```

- 각각의 페이지 내용은 `block content`의 하위에 추가하면 된다.

#### Partials

- 공통으로 쓰이는 일부분을 만들어놓고 불러서 사용한다. (header, footer 등)

```pug
//- header.pug
header
  .logo
    h1 LOGO
  ul
    li
      a(href='/login') Login
    li
      a(href='/Join') Join
  h3 Pug는 쉬워요!
```

```pug
//- footer.pug
footer
  span &copy; Footer
```

```pug
//- layouts/main.pug
doctype html
html
  head
    title Pug Template
  body
    include ../partials/header
    main
      //- 각각 페이지의 내용이 들어갈 부분
      block content
    include ../partials/footer
```

> 파일 구조는 위의 이미지를 참고.

- partials의 파일은 필요한 위치에 `include`시켜준다. (**파일 경로 중요!**)
