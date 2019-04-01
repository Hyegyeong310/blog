---
layout: post
title: '[Data Structure] Doubly Linked List'
author: HyeGyeong
categories: [dataStructure]
image: 'assets/images/6.jpeg'
---

# DoublyLinkedList

## 1. DoublyLinkedList란?

DoublyLinkedList는 LinkedList의 단점을 보완한 리스트이다.<br/>
LinkedList는 마지막 요소를 찾을 때 처음부터 끝까지 모두 탐색해야 하는 단점이 있었다.<br>
DoublyLinkedList는 양방향 탐색이 가능하여 찾는 인덱스를 사이즈의 절반과 비교하고 처음부터 비교하거나, 뒤에서부터 비교하는 식으로 탐색시간을 반으로 줄일 수 있다.<br>
하지만 LinkedList는 next를 담을 데이터 영역 하나가 필요한 반면, DoublyLinkedList는 prev를 담을 데이터 영역 하나가 더 필요하다.<br>

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2949.png">

> (출처: 생활코딩)

## 2. DoublyLinkedList 기능

### 2.1 데이터의 추가

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2958.png">
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2959.png">
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2960.png">
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2961.png">
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2962.png">
<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2963.png">

> (출처: 생활코딩)

DoublyLinkedList의 데이터 추가는 LinkedList와 거의 비슷하다. 다만 prev를 연결해주는 작업이 필요하다.<br>
그리고 그림과 같이 중간에 추가하는 경우에 추가할 인덱스와 (전체 사이즈 길이/2)를 비교하여 뒤에서 탐색할지 앞에서 탐색할지 결정할 수 있다.<br/>
JavaScript로 데이터 추가에 대한 구현은 다음과 같다.

```javascript
doublyLinkedList.prototype.addFirst = function(elem) {
  var node = new Node(elem);
  node.next = this.head;
  if (this.head != null) {
    // head가 null이 아니면 추가할 node와 연결이 필요하다.
    this.head.prev = node;
  }
  this.head = node; // head가 node를 가리키도록 바꾼다.
  this.size++;
  if (this.head.next.data === null) {
    //head.next가 없으면 값이 1개 있는 상태. tail과 head가 같은 데이터를 가리킨다.
    this.tail = this.head;
  }
};

doublyLinkedList.prototype.addLast = function(elem) {
  var node = new Node(elem);
  if (this.size === 0) {
    return this.addFirst(elem);
  } else {
    this.tail.next = node;
    node.prev = this.tail;
    this.tail = node;
    this.size++;
  }
};

doublyLinkedList.prototype.add = function(pos, elem) {
  if (pos === 0) {
    return this.addFirst(elem);
  } else {
    var node = new Node(elem);
    // 추가할 위치의 이전 노드를 찾는다. (추가할 위치에 있던 데이터 참조주소값을 갖고 있기 때문)
    var temp1 = this.findNode(pos - 1);
    var temp2 = temp1.next; // 추가할 위치에 있던 데이터
    temp1.next = node;
    node.prev = temp1;
    node.next = temp2;
    if (temp2 != null) {
      temp2.prev = node;
    }
    this.size++;
    if (node.next === null) {
      this.tail = node;
    }
  }
};
```

### 2.2 데이터의 삭제

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2969.png"><br/>
<code>삭제할 노드의 이전 노드를 찾아서 저장한다.</code>

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2970.png"><br/>
<code>삭제할 노드를 찾아서 저장한다.(return 값으로 사용)</code>

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2971.png"><br/>
<code>삭제할 노드의 다음 노드를 찾아서 저장한다.</code>

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2972.png"><br/>
<code>노드를 삭제한다.</code>

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2973.png"><br/>
<code>삭제된 노드의 이전 노드의 next를 삭제된 노드의 다음 노드로 연결한다.</code>

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2974.png"><br/>
<code>삭제된 노드의 prev를 삭제된 노드의 이전 노드로 연결한다.</code>

> (출처: 생활코딩)

삭제할 노드의 이전 노드와 다음 노드를 찾아서 둘을 연결해주면 된다. 삭제 역시 LinkedList와 비슷하다.

```javascript
// 첫번째 요소 삭제
doublyLinkedList.prototype.removeFirst = function() {
  var temp = this.head;
  this.head = temp.next; // head를 head의 다음 노드로 지정한다.
  var removed = temp.data;
  temp = null; // 데이터 삭제
  if (this.head != null) {
    this.head.prev = null;
  }
  this.size--;
  return removed; // 삭제된 값 리턴
};

// 원하는 위치 요소 삭제
doublyLinkedList.prototype.remove = function(pos) {
  if (pos === 0) {
    return this.removeFirst();
  } else {
    var temp = this.findNode(pos - 1); // 삭제될 노드 prev 저장
    var removed = temp.next;
    temp.next = removed.next; // 삭제될 노드 next 저장
    if (temp.next != null) {
      temp.next.prev = temp;
    }
    var removedData = removed.data;
    if (removed === this.tail) {
      // 삭제된 노드가 마지막 노드였다면 tail을 삭제된 노드의 prev로 수정해준다.
      this.tail = temp;
    }
    removed = null;
    this.size--;
    return removedData;
  }
};

// 마지막 요소 삭제
doublyLinkedList.prototype.removeLast = function() {
  return this.remove(size - 1);
};
```

### 2.3 데이터 탐색, 가져오기

인덱스가 (전체사이즈/2)보다 작으면 head에서 탐색, 크거나 같으면 tail에서 탐색하고, <br>
해당 인덱스의 노드를 리턴하는 findNode 함수를 이용하여 원하는 위치의 데이터 값을 쉽게 가져올 수 있다.

```javascript
// 노드 찾기
doublyLinkedList.prototype.findNode = function(index) {
  var x;
  if (index < this.size / 2) {
    x = this.head;
    for (var i = 0; i < index; i++) {
      x = x.next;
    }
  } else {
    x = this.tail;
    for (var i = index - 1; i > index; i--) {
      x = x.prev;
    }
  }
  return x;
};

// 데이터 가져오기
doublyLinkedList.prototype.get = function(pos) {
  var temp = this.findNode(pos);
  return temp.data;
};

// 데이터 탐색
doublyLinkedList.prototype.indexOf = function(data) {
  var temp = this.head;
  var index = 0;
  while (temp.data != data) {
    temp = temp.next;
    index++;
    if (temp === null) {
      return -1; // 해당 데이터가 없으면 -1 리턴
    }
  }
  return index; // 있으면 해당 인덱스 리턴
};
```

### 2.4 데이터 reverse

<img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2968.png" />

> (출처: 생활코딩)
> LinkedList는 데이터 reverse를 하려면 next의 위치를 반대로 바꿔야했다. DoublyLinkedList는 양방향 탐색이 가능해서 prev를 이용하면 된다.<br/>
