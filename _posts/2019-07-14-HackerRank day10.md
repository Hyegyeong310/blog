---
layout: post
title: '[Algorithm] HackerRank day10'
author: HyeGyeong
categories: [algorithm]
image: 'assets/images/algorithm.jpg'
sitemap:
  changefreq: daily
  priority: 1.0
---

Today, we're working with binary numbers. Check out the Tutorial tab for learning materials and an instructional video!

#### Task

Given a base-10 integer, `n`, convert it to binary (base-2). Then find and print the base-10 integer denoting the maximum number of consecutive 1's in n's binary representation.

#### Input Format

A single integer, n.

#### Constraints

- `1 ≤ n ≤ 10^6`

#### Output Format

Print a single base-10 integer denoting the maximum number of consecutive 1's in the binary representation of n.

#### Sample Input 1

```
5
```

#### Sample Output 1

```
1
```

#### Sample Input 2

```
13
```

#### Sample Output 2

```
2
```

#### Explanation

Sample Case 1:
The binary representation of `5` is `101`, so the maximum number of consecutive 1's is `1`.

Sample Case 2:
The binary representation of `13` is `1101`, so the maximum number of consecutive 1's is `2`.

## Solve

- 10진수 n을 2진수로 바꿨을 때 1의 개수가 연속되는 수를 구하는 것.
- 10진수 `5`를 2진수로 바꾸면 `101`이고 연속되는 1의 개수는 1개.
- 10진수 `13`을 2진수로 바꾸면 `1101`이고 연속되는 1의 개수는 2개.
- 10진수를 2진수로 바꿔서 연속되는 1의 개수를 세려고 했는데 2로 나눈 나머지가 1이면 1, 아니면 0이기 때문에 n이 더 이상 나눌 수 없을 때까지 나누면서 1이 연속되는지 아닌지만 체크하면 된다.

```ts
function main(n: number): number {
  let count: number = 0,
    max: number = 0;

  while (n > 0) {
    if (n % 2 === 1) {
      count++;
    } else {
      count = 0;
    }
    max = Math.max(count, max);
    n = Math.floor(n / 2);
  }

  console.log(max);
  return max;
}
```

> [출처: [https://www.hackerrank.com](https://www.hackerrank.com)]
