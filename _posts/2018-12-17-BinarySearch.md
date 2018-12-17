---
layout: post
title: "[Sorts] Binary Search"
author: HyeGyeong
categories: [Sorts]
image: "assets/images/9.jpeg"
---

# Binary Search

## 1. Binary Search란?

한국어로 '이진탐색'을 말한다. 이진탐색은 정렬된 상태에서만 사용할 수 있다.<br>
중간값과 내가 찾는 데이터를 비교하고 중간값보다 작으면 왼쪽, 중간값보다 크면 오른쪽으로 탐색을 다시 한다.<br>
중간값보다 작은 경우일 때, 왼쪽 값들의 중간값을 찾아서 다시 비교한다.<br>
여기서도 작으면 왼쪽, 크면 오른쪽으로 가면서 탐색을 계속한다. 코드 상으로는 찾는 데이터가 없으면 -1, 있으면 그 데이터의 인덱스를 리턴한다.

<img src="https://t1.daumcdn.net/cfile/tistory/262CCF4657D6D0352E"><br>

> (출처: Hanmo's IT)

JavaScript로 이진탐색에 대한 구현은 다음과 같다.

```javascript
// 배열 정렬
ArrayList.prototype.sort = function(){
  this.array.sort(function(a,b){
    return a-b;
  });
} // 오름차순 정렬

// 이진탐색
ArrayList.prototype.binarySearch = function(data, first, last){
  var middleIndex = 0;
  while(first <= last){ // first가 last보다 작거나 같으면 반복.
    middleIndex = Math.floor((first+last)/2); // middleIndex에 중간값 할당. Math.floor를 이용해서 소수점 버림
    if(data === this.array[middleIndex]){
      return middleIndex; // 중간값과 같으면 중간값 인덱스 리턴
    } else {
      if(data < this.array[middleIndex]){ // data가 중간값보다 작으면 왼쪽에서 탐색
        return this.binarySearch(data, first, middleIndex-1); // 재귀함수(first = 0; last = 중간값-1)
      } else {
        return this.binarySearch(data, middleIndex+1, last); // 재귀함수 (first = 중간값+1; last = 배열길이-1)
      }
    }
  }
  return -1; // 데이터가 없으면 -1 리턴
}

var list = new ArrayList();
list.pushFirst(11);
list.pushFirst(9);
list.push(0, 5);
list.pushLast(3);
list.pushLast(12);
list.pushLast(6);
list.pushLast(8);
list.pushLast(2);
list.toString(); // [5, 9, 11, 3, 12, 6, 8, 2]
list.sort();
list.toString(); // [2, 3, 5, 6, 8, 9, 11, 12]
list.binarySearch(9, 0, list.size-1)); // 5
```
