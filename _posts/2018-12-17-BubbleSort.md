---
layout: post
title: '[Sorts] Bubble Sort'
author: HyeGyeong
categories: [Sorts]
image: 'assets/images/11.jpeg'
---

# Bubble Sort

## 1. Bubble Sort란?

한국어로 '버블정렬 (거품정렬)'을 말한다. 인접한 두 요소를 비교하여 정렬하는데<br>
거품이 보글보글 떠오르는 것과 비슷하다 하여 거품정렬이라 한다.<br>
리스트의 왼쪽에서 오른쪽 끝까지 진행하는데 모두 정렬될 때까지 반복하기 때문에<br>
비효율적인 정렬이다. 하지만 단순해서 많이 이용한다고 한다.

<img src="https://t1.daumcdn.net/cfile/tistory/275F9A4A545095BD01"><br>

> (출처: 배고파서 까먹고 만든 블로그)

JavaScript로 구현한 코드는 다음과 같다. (이중연결리스트 이용)

```javascript
doublyLinkedList.prototype.bubbleSort = function() {
  var temp = this.head;
  for (var i = 0; i < this.size - 1; i++) {
    if (temp.data > temp.next.data) {
      // 현재 temp 데이터가 next 데이터보다 크면
      this.swap(temp, temp.next); // swap 함수를 이용하여 교환한다.
    }
    temp = temp.next; // temp에 다음 node 할당. 이렇게 이중연결리스트 길이만큼 반복
  }
};

doublyLinkedList.prototype.swap = function(node1, node2) {
  var temp = node1.data; // node1의 데이터 할당
  node1.data = node2.data; // node1의 데이터를 node2의 데이터로 할당
  node2.data = temp; // node2의 데이터를 node1의 데이터를 갖고 있는 temp로 할당
};
```
