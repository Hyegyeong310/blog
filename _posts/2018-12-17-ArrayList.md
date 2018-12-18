---
layout: post
title: "[Data Structure] ArrayList"
author: HyeGyeong
categories: [dataStructure]
image: "assets/images/4.jpeg"
---

# ArrayList

## 1. ArrayList란?

배열을 이용하여 리스트를 구현한 것이다. 장점은 인덱스를 이용하여 접근할 수 있어 원하는 데이터를 가져오는 것이 빠르게 처리된다는 점이고, 단점은 데이터가 추가, 삭제될 경우 그 해당 인덱스 이후의 데이터들을 하나하나 이동시켜야하기 때문에 느리다는 것이다.<br/>
즉, 추가/삭제가 별로 없고 검색을 많이 하는 경우 사용하면 좋다.

## 2. ArrayList 기능

### 2.1 데이터의 추가

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2886.png" />

> (출처: 생활코딩)

ArrayList는 내부적으로 데이터를 배열에 저장한다. 데이터를 리스트의 처음이나 중간에 추가하면, 이후의 데이터들이 한칸씩 뒤로 물러나야한다.<br/>
JavaScript로 데이터 추가에 대한 구현은 다음과 같다.

```javascript
// 첫번째 자리에 요소 추가
List.prototype.addFirst = function(element) {
  return this.add(0, element);
};

// 원하는 위치에 요소 추가
List.prototype.add = function(index, element) {
  this.extendLen();
  for (var i = this.arraySize - 1; i >= index; i--) {
    this.arrayList[i + 1] = this.arrayList[i];
  }
  this.arrayList[index] = element;
  this.arraySize++; // 데이터 개수 체크용
  return this.arrayList;
};

// 마지막 자리에 요소 추가
List.prototype.addLast = function(element) {
  this.extendLen();
  this.arrayList[this.arraySize] = element;
  this.arraySize++;
  return this.arrayList;
};
```

### 2.2 데이터의 삭제

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2887.png" />

> (출처: 생활코딩)

추가와 마찬가지로 ArrayList는 비어있는 데이터가 없어야하기 때문에 삭제된 이후의 데이터를 하나하나 앞으로 이동시켜야 한다.

```javascript
// 요소 삭제
List.prototype.remove = function(index) {
  var removed = this.arrayList[index]; // 삭제될 요소를 return해주기 때문에 삭제되기 전에 담아둔다.
  for (var i = index; i <= this.arraySize; i++) {
    this.arrayList[i] = this.arrayList[i + 1];
  }
  this.arraySize--;
  this.arrayList[this.arraySize] = null;
  if (this.arraySize >= this.arrLength) {
    this.arrLength--;
  }
  return removed;
};
```

### 2.3 데이터 가져오기

<code>numbers.get(2);</code><br/>
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2891.png" />

> (출처: 생활코딩)

ArrayList의 장점은 여기에서 드러난다. 원하는 인덱스의 데이터를 바로 가져올 수 있다.

```javascript
// 요소 가져오기
List.prototype.get = function(index) {
  return this.arrayList[index];
};
```

### 2.4 데이터 검색

ArrayList 내에 내가 찾는 데이터가 있는지 확인하는 기능이다. 있다면 해당 데이터의 인덱스를, 없다면 -1을 반환한다.

```javascript
// 요소 찾기
List.prototype.find = function(element) {
  for (var i = 0; i < this.arraySize; i++) {
    if (this.arrayList[i] === element) {
      return i; // 해당 데이터와 일치하는 인덱스 반환.
    }
  }
  return -1; // 일치하는 데이터가 없으면 -1을 반환.
};
```
