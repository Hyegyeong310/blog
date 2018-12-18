---
layout: post
title: "[Sorts] Selection Sort & Insertion Sort"
author: HyeGyeong
category: Sorts
image: "assets/images/10.jpeg"
---

# Selection Sort

## 1. Selection Sort란?

한국어로 '선택정렬'을 말한다. 선택정렬은 갖고 있는 값 중 가장 작은 값을 먼저 선택하고 맨 앞의 값과 교체한다.<br>
그 이후엔 맨 앞자리를 제외한 나머지 리스트 중 가장 작은 값을 선택한 뒤 두번째 자리 값과 교체한다.<br>
나머지 값들이 정렬될 때까지 반복한다.

<img src="https://t1.daumcdn.net/cfile/tistory/256B9C34545081D835"><br>

> (출처: 배고파서 까먹고 만든 블로그)

JavaScript로 선택정렬에 대한 구현은 다음과 같다.

```javascript
// 값 교환해주는 함수
var swap = function(arr, index1, index2) {
  var temp = arr[index1];
  arr[index1] = arr[index2];
  arr[index2] = temp;
};

var selectionSort = function(arr) {
  var minElem, temp;
  for (var i = 0; i < arr.length; i++) {
    // 0부터 arr길이만큼 반복
    minElem = arr[i]; // minElem을 구할 기준
    temp = i; // 교환할 인덱스 할당
    for (var j = i + 1; j < arr.length; j++) {
      // 1부터 arr길이만큼 반복
      if (minElem > arr[j]) {
        // 첫번째 요소를 제외한 값 중 더 작은 값이 있으면
        minElem = arr[j]; // minElem으로 다시 할당.
        temp = j; // 교환할 인덱스 재할당
      }
    }
    swap(arr, i, temp); // i=0일 때 0번째 요소와 최소값 교환
  }
  return arr;
};
```

# Insertion Sort

## 2. Insertion Sort란?

한국어로 '삽입정렬'을 말한다. 삽입정렬은 앞에서부터 정렬을 시작하는데 뒤의 값이 앞에 정렬된 값 사이에 속하면 그 자리를 찾아 삽입하는 정렬이다.<br>
이미 정렬된 앞의 정렬을 다시 검색하여 값을 넣어야 하기 때문에 배열의 길이가 길면 비효율적이다.

<img src="https://t1.daumcdn.net/cfile/tistory/2569FD3854508BE811"><br>

> (출처: 배고파서 까먹고 만든 블로그)

JavaScript로 삽입정렬에 대한 구현은 다음과 같다.

```javascript
// 값 교환해주는 함수
var swap = function(arr, index1, index2) {
  var temp = arr[index1];
  arr[index1] = arr[index2];
  arr[index2] = temp;
};

var insertionSort = function(arr) {
  for (var i = 1; i < arr.length; i++) {
    // 1번부터 배열 길이만큼 반복
    if (arr[i - 1] > arr[i]) {
      // 이전 요소가 다음 요소보다 크면
      for (var j = 0; j < i; j++) {
        // 0번부터 i까지 반복
        if (arr[j] > arr[i]) {
          // 자리를 찾는 요소가 정렬된 요소보다 작으면 교환
          swap(arr, i, j);
        }
      }
    }
  }
  return arr;
};
```
