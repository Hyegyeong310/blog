---
layout: post
title: '[기술] 벤더 프리픽스 (Vendor Prefix)'
author: HyeGyeong
categories: [technical]
image: 'assets/images/technical.jpg'
---

### 벤더 프리픽스 (Vendor Prefix)

- 현재 국내의 브라우저는 익스플로러, 크롬, 오페라, 파이어폭스, 사파리 등이 있다. CSS3로 발전하면서 그 경계가 많이 허물어 졌지만 아직 남아있는 각 브라우저별로 따로 놀던 CSS3의 속성을 잡아주기 위해 생긴 접두어를 **벤더 프리픽스**라 한다.
- ```
    -webkit-: 구글, 사파리
    -moz-: 파이어폭스
    -o-: 오페라
    -ms-: 익스플로러 (생략 가능)

    // Example
    -webkit-border-radius: 10px;
    -moz-​border-radius: 10px;
    -o-​border-radius: 10px;
    -ms-border-radius: 10px;
    border-radius: 10px;
  ```

- CSS는 위에서부터 읽히기 때문에 벤더 프리픽스가 필요한 브라우저 속성을 적은 뒤 표준속성을 쓰면 된다. 각 벤더 프리픽서를 이해하지 못하는 브라우저는 그 속성을 무시하고, 표준을 지원하는 브라우저는 맨 마지막의 속성을 실행한다.
  > 참고사이트: [Can I Use](https://caniuse.com/)

### 크로스 브라우징 (Cross Browsing)

- W3C에서 채택된 표준 웹 기술을 적용해 모든 브라우저에서 이상없이 작동되게 웹페이지를 제작하는 방법론.
- 다양한 브라우저를 이용하더라도 사이트를 100% 이용할 수 있게 만드는 기술.
- 크로스 브라우징은 `모든 브라우저에서 똑같이 보이게 하는 것`이 아닌 **`모든 브라우저에 동등성을 부여하는 것`**.

### 핵 (Hack)

- 모든 CSS 속성이 모든 브라우저에서 똑같이 보이지 않는다. (특히 IE...) 이런 특성을 이용해 특정 브라우저를 제외 또는 특정 브라우저에서만 CSS를 적용하는 기법을 **핵**이라 한다.
- 문법적으로 맞지 않거나, 특정 브라우저에서만 적용되는 비표준인 경우가 많아, CSS 핵은 정말 꼭!!! 써야 하는 경우가 아니면 사용하지 말자!
- 핵 사용법은 따로 정리해서 올릴 예정. IE에 적용하는 핵이 굉장히 많다...IE 일 좀 해라...
