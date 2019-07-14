---
layout: post
title: '[Algorithm] HackerRank day11'
author: HyeGyeong
categories: [algorithm]
image: 'assets/images/algorithm.jpg'
sitemap:
  changefreq: daily
  priority: 1.0
---

Today, we're building on our knowledge of Arrays by adding another dimension. Check out the Tutorial tab for learning materials and an instructional video!

#### Context

Given a 6 × 6 2D Array, `A`:

```js
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
```

We define an hourglass in `A` to be a subset of values with indices falling in this pattern in `A`'s graphical representation:

```js
a b c
  d
e f g
```

There are `16` hourglasses in `A`, and an hourglass sum is the sum of an hourglass' values.

#### Task

There are `6` lines of input, where each line contains `6` space-separated integers describing 2D Array `A`; every value in `A` will be in the inclusive range of `-9` to `9`.

#### Constraints

- `-9 ≤ A[i][j] ≤ 9`
- `0 ≤ i,j ≤ 5`

#### Output Format

Print the largest (maximum) hourglass sum found in `A`.

#### Sample Input

```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 2 4 4 0
0 0 0 2 0 0
0 0 1 2 4 0
```

#### Sample Output

```
19
```

#### Explanation

`A` contains the following hourglasses:

```
1 1 1   1 1 0   1 0 0   0 0 0
  1       0       0       0
1 1 1   1 1 0   1 0 0   0 0 0

0 1 0   1 0 0   0 0 0   0 0 0
  1       1       0       0
0 0 2   0 2 4   2 4 4   4 4 0

1 1 1   1 1 0   1 0 0   0 0 0
  0       2       4       4
0 0 0   0 0 2   0 2 0   2 0 0

0 0 2   0 2 4   2 4 4   4 4 0
  0       0       2       0
0 0 1   0 1 2   1 2 4   2 4 0
```

The hourglass with the maximum sum (`19`) is:

```
2 4 4
  2
1 2 4
```

## Solve

- 모래시계 형태의 수가 6 × 6 arr에 있을 때 가장 큰 합을 return한다.
- 모래시계 형태로 직접 넣어서 합을 구했는데 더 좋은 방법이 있는지 고민할 것.

```js
function main() {
  let arr = Array(6);
  let maxTotal;

  // 문제에 입력된 수를 6 × 6 Array 형태로 만들어주는 부분
  for (let i = 0; i < 6; i++) {
    arr[i] = readLine()
      .split(' ')
      .map(arrTemp => parseInt(arrTemp, 10));
  }

  for (let i = 0; i < arr.length - 2; i++) {
    for (let j = 0; j < arr.length - 2; j++) {
      // hourglasses 형태를 갖춘 위치의 수를 모두 합함.
      let total =
        arr[i][j] +
        arr[i][j + 1] +
        arr[i][j + 2] +
        arr[i + 1][j + 1] +
        arr[i + 2][j] +
        arr[i + 2][j + 1] +
        arr[i + 2][j + 2];

      if (!maxTotal && maxTotal !== 0) {
        maxTotal = total;
      }
      if (total > maxTotal) {
        maxTotal = total;
      }
    }
  }
  console.log(maxTotal);
  return maxTotal;
}
```

> [출처: [https://www.hackerrank.com](https://www.hackerrank.com)]
