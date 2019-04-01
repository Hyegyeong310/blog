---
layout: post
title: '[Sorts] Merge Sort'
author: HyeGyeong
categories: [Sorts]
image: 'assets/images/12.png'
---

# Merge Sort

## 1. Merge Sort란?

한국어로 '병합정렬 (합병정렬)'을 말한다. '존 폰 노이만(John von Neumann)'이라는 사람이 제안한 방법이다.<br>
분할정복 알고리즘의 하나로, 하나의 리스트를 두 개의 균등한 크기로 분할하고 분할된 리스트를 정렬한 다음, <br>
두 개의 정렬된 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다.

## 2. 병합정렬 작동 방법

1. 리스트의 길이가 0 또는 1이면 이미 정렬된 것으로 본다.
2. 그 외에는 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 리스트 2개로 나눈다.
3. 각 부분 리스트를 재귀적으로 병합정렬을 이용하여 정렬한다.
4. 2개의 리스트를 다시 하나의 정렬된 리스트로 합병한다.

<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif"><br>

> (출처: 위키백과)

<img src="https://gmlwjd9405.github.io/images/algorithm-merge-sort/merge-sort-concepts.png">

> (출처: Heee's Development Blog)

JavaScript로 구현한 코드는 다음과 같다.

```javascript
var mergeSort = function(arr) {
  var len = arr.length;
  if (len === 1) {
    // array 길이가 1이면 그대로 반환
    return arr;
  }
  var middle = Math.floor(len / 2);
  var left = arr.slice(0, middle); // 0부터 middle 전까지 배열 복사
  var right = arr.slice(middle); // middle부터 끝까지 배열 복사
  var merge = function(left, right) {
    // mergeSort 함수 안의 merge 함수 선언
    var result = []; // merge에서 반환할 리스트 선언
    while (left.length && right.length) {
      // left, right 모두 빈 배열이 아니면(0은 falsy한 값. false로 친다)
      if (left[0] <= right[0]) {
        // left 첫번째 요소가 right 첫번째 요소보다 작거나 같으면
        result.push(left.shift()); // left 첫번째 요소를 result에 추가한다. left.length는 -1
      } else {
        result.push(right.shift()); // 아니면 right 첫번째 요소를 result에 추가한다. right.length는 -1
      }
    } // left 또는 rigth 길이가 0이 되면 다음 while문 진행
    while (left.length) {
      result.push(left.shift());
    }
    while (right.length) {
      result.push(right.shift());
    }
    return result;
  };
  return merge(mergeSort(left), mergeSort(right)); // 재귀함수 이용. 정렬될 때까지 반복.
};
```
