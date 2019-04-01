---
layout: post
title: '[Sorts] Quick Sort'
author: HyeGyeong
categories: [Sorts]
image: 'assets/images/13_1.jpg'
---

# Quick Sort

## 1. Quick Sort란?

퀵 정렬이란 분할정렬 중의 하나로 불안정 정렬에 속한다. 평균적으로 빠른 정렬이다.<br>
합병정렬과 비슷하게 분할을 하지만 합병정렬은 균등하게 분할을 해서 비교 정렬 했다면<br>
퀵 정렬은 비균등하게 분할을 해서 비교하는 것이 특징이다.<br>
하지만 정렬된 배열에 대해서는 불균등하게 분할함으로 인해 시간이 더 걸릴 수 있다.<br>

## 2. 퀵 정렬 작동 방법

1. 리스트의 길이가 0 또는 1이면 더이상 분할이 불가능하므로 반환한다.
2. 그 외에는 피봇(pivot)을 정하고 피봇과 비교하여 작으면 왼쪽, 크면 오른쪽으로 이동시킨다.
3. 피봇을 제외한 왼쪽 리스트와 오른쪽 리스트를 퀵 정렬을 재귀적으로 이용하여 다시 정렬한다.
4. 정렬된 리스트들을 피봇을 포함하여 하나의 리스트로 합친다.

<img src="https://gmlwjd9405.github.io/images/algorithm-quick-sort/quick-sort.png"><br>

> (출처: Heee's Development Blog)

JavaScript로 구현한 코드는 다음과 같다.

```javascript
var QuickSort = function(arr) {
  var newArr = arr.slice(); // arr copy
  var len = newArr.length; // 배열 길이
  if (len === 0) {
    // 빈 배열이면 [] 리턴
    return [];
  }
  var pivot = newArr[0]; // 피봇은 arr의 0번 인덱스 요소로 할당.
  var left = [],
    right = []; // left 빈배열 할당, right 빈배열 할당
  for (var i = 1; i < len; i++) {
    // 피봇 제외. 피봇 다음 인덱스부터 마지막 인덱스까지
    if (newArr[i] < pivot) {
      // 피봇보다 작으면
      left.push(newArr[i]); // left push
    } else {
      right.push(newArr[i]); // 크거나 같으면 right push
    }
  }
  return QuickSort(left).concat(pivot, QuickSort(right));
  // 재귀함수 이용. 빈배열이 나올 때까지 반복 후 concat으로 하나의 배열 리턴
};
```
