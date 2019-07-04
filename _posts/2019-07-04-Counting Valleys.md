---
layout: post
title: '[Algorithm] Counting Valleys'
author: HyeGyeong
categories: [algorithm]
image: 'assets/images/Counting-Valleys.jpg'
sitemap:
  changefreq: daily
  priority: 1.0
---

Gary is an avid hiker. He tracks his hikes meticulously, paying close attention to small details like topography. During his last hike he took exactly `n` steps. For every step he took, he noted if it was an uphill, `U`, or a downhill, `D` step. Gary's hikes start and end at sea level and each step up or down represents a `1` unit change in altitude. We define the following terms:

- A mountain is a sequence of consecutive steps above sea level, starting with a step up from sea level and ending with a step down to sea level.
- A valley is a sequence of consecutive steps below sea level, starting with a step down from sea level and ending with a step up to sea level.

Given Gary's sequence of up and down steps during his last hike, find and print the number of valleys he walked through.

For example, if Gary's path is `s = [DDUUUUDD]`, he first enters a valley `2` units deep. Then he climbs out an up onto a mountain `2` units high. Finally, he returns to sea level and ends his hike.

#### Function Description

Complete the countingValleys function in the editor below. It must return an integer that denotes the number of valleys Gary traversed.

countingValleys has the following parameter(s):

- n: the number of steps Gary takes
- s: a string describing his path

#### Input Format

The first line contains an integer `n`, the number of steps in Gary's hike.
The second line contains a single string `s`, of `n` characters that describe his path.

#### Constraints

- `2 ≤ n ≤ 10^6`
- `s[i] ∈ {UD}`

#### Output Format

Print a single integer that denotes the number of valleys Gary walked through during his hike.

#### Sample Input

```
8
UDDDUDUU
```

#### Sample Output

```
1
```

#### Explanation

If we represent \_ as sea level, a step up as /, and a step down as \, Gary's hike can be drawn as:

```
_/\      _
   \    /
    \/\/
```

He enters and leaves one valley.

## Solve

- 영어가 부족해서 문제 이해하는데 한참 걸렸음. **영어 공부하자ㅜㅜ**
- n은 step(그냥 path 하나 당 1 step으로 이해함)에 대한 Number, s는 path(U => Up, D => Down)에 대한 String.
- sea level보다 높고 up, down이 있으면 mountain.
- sea level보다 낮고 up, down이 있으면 valley.
- sea level을 0으로 봤을 때 U는 +1, D는 -1. 더하고 빼면서 이전 sea level이 음수이고 sea level이 0이 되는 시점에 valley count 1 증가.

```ts
function countingValleys(n: number, s: string): number {
  let countValley = 0;
  let seaLevel = 0;

  for (let i = 0; i < n; i++) {
    let preSeaLevel = seaLevel;
    if (s[i] === 'U') {
      seaLevel++;
    } else {
      seaLevel--;
    }
    if (seaLevel === 0 && preSeaLevel < 0) {
      countValley++;
    }
  }
  return countValley;
}
```

> [출처: [https://www.hackerrank.com](https://www.hackerrank.com)]
