---
layout: post
title: "[Data Structure] LinkedList"
author: HyeGyeong
category: dataStructure
image: "assets/images/5.jpeg"
---

# LinkedList

## 1. LinkedList란?

LinkedList는 ArrayList와 다르게 요소와 요소 사이를 링크로 연결한 리스트이다. <br/>
둘 다 크기에 제한은 없지만 기능의 차이가 있다.<br/>
ArrayList는 배열을 기반으로 만들어진 리스트이기 때문에 정해져있는 배열이 꽉 차면 그 배열의 2배크기의 배열을 새로 만들어서 데이터를 옮긴다.<br/>
LinkedList는 요소 사이를 링크로 이어주기만 하면 되기 때문에 크기에 제한이 없다.<br/>
하지만 검색을 하는 경우 각 요소가 다음 요소만을 알고 있기 때문에 모든 요소를 훑어 올라가야한다.
마지막 요소를 검색해야 하는 경우 첫번째 요소부터 마지막 요소까지 봐야하기 때문에 이 경우가 최악의 경우이다.
그러므로 검색이 별로 없고 추가/삭제를 많이 하는 경우 사용하면 좋다.
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2939.png" />

> (출처: 생활코딩)

## 2. LinkedList 기능

### 2.1 데이터의 추가

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2922.png" />
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2923.png" />
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2924.png" />
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2926.png" />

> (출처: 생활코딩)

ArrayList와 LinkedList의 핵심적인 차이는 여기에서 드러난다. <br/>
배열은 요소를 중간에 추가/삭제하면 그 요소 뒤의 요소들을 한칸씩 이동해야했다. 그래서 ArrayList는 추가/삭제가 많은 경우에 맞지 않는다.<br/>
하지만 LinkedList는 추가/삭제가 될 요소의 이전 요소 next(참조 주소값)를 바꾸면 되기 때문에 속도가 빠르다.<br/>
JavaScript로 데이터 추가에 대한 구현은 다음과 같다.

```javascript
var LinkedList = function() {
  this.length = 0; // 요소 개수 체크
  this.head = null; // 첫번째 요소의 참조 주소값 저장
};

var Node = function(elem) {
  this.data = elem;
  this.next = null;
};

LinkedList.prototype.addFirst = function(elem) {
  return this.add(0, elem);
};

LinkedList.prototype.add = function(index, elem) {
  var node = new Node(elem);
  var curr = this.head;
  var prev;
  var i = 0;

  if (index >= 0 && index <= this.length) {
    if (index === 0) {
      node.next = curr;
      this.head = node;
    } else {
      while (i++ < index) {
        prev = curr;
        curr = curr.next;
      }
      node.next = curr;
      prev.next = node;
    }
    this.length++;
    return LinkedList;
  }
  return false;
};

LinkedList.prototype.addLast = function(elem) {
  return this.add(this.length, elem);
};
```

### 2.2 데이터의 삭제

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2934.png"><br/>
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2935.png"><br/>
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2936.png"><br/>

> (출처: 생활코딩)

삭제할 요소의 이전 노드가 삭제요소의 다음 노드를 가리키게 하면 삭제할 요소의 주소값을 가진 요소가 없기 때문에 없는 요소나 다름 없다.<br>
즉, 삭제할 요소 외에 다른 요소들을 모두 연결해주면 삭제할 수 있다.

```javascript
// 첫번째 요소 삭제
LinkedList.prototype.removeFirst = function() {
  return this.remove(0);
};

// 요소 삭제
LinkedList.prototype.remove = function(index) {
  var curr = this.head;
  var prev;
  var i = 0;
  if (index === 0) {
    this.head = curr.next;
  } else {
    while (i++ < index) {
      prev = curr;
      curr = prev.next;
    }
    prev.next = curr.next;
  }
  curr.next = null;
  this.length--;
  return curr.data;
};

// 마지막 요소 삭제
LinkedList.prototype.removeLast = function() {
  return this.remove(this.length - 1);
};
```

### 2.3 데이터 검색

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2938.png"><br/>
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2937.png">

> (출처: 생활코딩)

LinkedList는 자신과 다음 요소밖에 모르기때문에 위의 그림과 같이 마지막 요소를 검색하려면 처음부터 마지막까지 찾아야한다.<br>
데이터 양이 많고 조회가 많은 경우엔 ArrayList에 비해 시간이 오래 걸린다.

```javascript
// 데이터 검색
LinkedList.prototype.indexOf = function(elem) {
  var temp = this.head; // 첫번째 요소 지정
  var index = 0;
  while (temp.data != elem) {
    temp = temp.next;
    index++;
    if (temp === null) {
      // temp가 null인 것은 temp의 이전 요소가 마지막 요소라는 뜻.
      return -1;
    }
  }
  return index;
};
```

### 2.4 데이터 reverse

<img src="https://postfiles.pstatic.net/MjAxODA1MjNfMTk1/MDAxNTI3MDQ4NTQ1Njgy.oqanuP2mcg2e0XZovLcbKQIAi6PNieoDW035IpWD47wg.GbLaZprxvP1s9-Efb3qhqkk--9_7Has07DdQteHy9OMg.PNG.rat5730/image_361921741527048536721.png?type=w773"></br>
데이터를 반전시키는 기능이다. next의 주소값을 이전 요소로 바꿔주면 된다.<br>
기존 요소를 저장해놓고 참조 주소값를 반대로 변경해주고 다시 기존의 주소를 넣어주는 반복을 행하면 reverse 된다.<br/>

```javascript
// 요소 찾기
LinkedList.prototype.reverse = function() {
  var curr = this.head;
  var next = null,
    prev = null;
  while (curr) {
    next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }
  this.head = prev;
};
```
