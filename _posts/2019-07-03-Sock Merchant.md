---
layout: post
title: '[Algorithm] Sock Merchant'
author: HyeGyeong
categories: [algorithm]
image: 'assets/images/sock-merchant.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

John works at a clothing store. He has a large pile of socks that he must pair by color for sale. Given an array of integers representing the color of each sock, determine how many pairs of socks with matching colors there are.

For example, there are `n = 7` socks with colors `ar = [1, 2, 1, 2, 1, 3, 2]`. There is one pair of color 1 and one of color 2. There are three odd socks left, one of each color. The number of pairs is 2.

#### Function Description

Complete the sockMerchant function in the editor below. It must return an integer representing the number of matching pairs of socks that are available.

sockMerchant has the following parameter(s):

- n: the number of socks in the pile
- ar: the colors of each sock

#### Input Format

The first line contains an integer `n`, the number of socks represented in `ar`.
The second line contains `n` space-separated integers describing the colors `ar[i]` of the socks in the pile.

#### Constraints

- 1 ≤ n ≤ 100
- 1 ≤ ar[i] ≤ 100 where 0 ≤ i < n

#### Output Format

Return the total number of matching pairs of socks that John can sell.

#### Sample Input

```
9
10 20 20 10 10 30 50 10 20
```

#### Sample Output

```
3
```

#### Explanation

![image](https://user-images.githubusercontent.com/25483027/60596907-e44f0900-9de4-11e9-8684-6b0a62bca1c9.png)
John can match three pairs of socks.

## Solve

- 같은 숫자끼리 쌍을 이루도록 모아야 한다.
- 2개씩 짝을 지어주고 남은 것은 count되지 않도록 해야 한다.
- sort 메소드를 이용해 오름차순으로 정렬해서 2개씩 묶어주고 count는 1씩 증가, 2개의 짝이 만들어지면 i에 1을 더해서 이미 짝지어진 양말은 통과시킨다.

```js
function sockMerchant(n, ar) {
  let count = 0;
  ar = ar.sort();
  for (let i = 0; i < n - 1; i++) {
    // Or for(let i = 0; i < ar.length-1; i++)
    if (i < n && ar[i] === ar[i + 1]) {
      count++;
      i += 1;
    }
  }
  return count;
}
```

> [출처: [https://www.hackerrank.com](https://www.hackerrank.com)]
