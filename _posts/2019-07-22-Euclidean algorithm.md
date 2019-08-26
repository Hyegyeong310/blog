---
layout: post
title: '[Algorithm] 유클리드 호제법'
author: HyeGyeong
categories: [algorithm]
image: 'assets/images/Euclidean.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

### 개요

- 두 양의 정수, 혹은 두 다항식의 최대 공약수를 구하는 방법. 호제법은 서로(互)를 나누기(除) 때문에 붙은 이름.
- 최대공약수를 구하는 문제를 풀면서 처음 알았다.
- `쵀대공약수 알고리즘`으로 검색하면 가장 위에 나오는 게 유클리드 호제법.

```
두 양의 정수 a, b (b > a)에 대하여 b = aq + r, (0 ≤ r < a)라 하면, a, b의 최대공약수는 a, r의 최대공약수와 같다. 즉 gcd(a, b) = gcd(a, r).
> gcd: greatest common divisor
```

> [출처: [나무위키 - 유클리드 호제법](https://bit.ly/2YZoLzH)]

### 유클리드 호제법 사용

- gcd (2개의 정수에 대한 최대공약수)

```js
const gcd = numArr => {
  let a = numArr[0],
    b = numArr[1],
    r = 0;
  while (b !== 0) {
    r = a % b;
    a = b;
    b = r;
  }
  return a;
};
```

- multipleGcd (2개 이상의 정수에 대한 최대공약수)

```js
const multipleGcd = numArr => {
  let result = gcd([numArr[0], numArr[1]]);
  for (let i = 2; i < numArr.length; i++) {
    result = gcd([result, numArr[i]]);
  }
  return result;
};
```
