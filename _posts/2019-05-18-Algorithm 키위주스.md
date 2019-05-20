---
layout: post
title: '[Algorithm] 키위주스'
author: HyeGyeong
categories: [Algorithm]
image: 'assets/images/kiwi_juice.jpeg'
---

## 01 >> 키위주스

**원문)**  
Taro has prepared delicious kiwi fruit juice. He poured it into N bottles numbered from 0 to N-1. The capacity of the i-th bottle is capacities[i] liters, and he poured bottles[i] liters of kiwi juice into this bottle.  
Now he wants to redistribute juice in the bottles. In order to do this, he will perform M operations numbered from 0 to M-1 in the order in which he will perform them. For the i-th operation, he will pour kiwi juice from bottle from Id[i] to bottle toId[i]. He will stop pouring when bottle fromId[i] becomes empty or bottle toId[i] becomes full, whichever happens earlier.  
Return an int[] that contains exactly N elements and whose i-th element is the amount of kiwi juice in the i-th bottle after all pouring operations are finished.  
<br/>
**번역)**  
타로는 맛있는 키위 주스를 준비했습니다. 타로는 0부터 N-1이라 이름을 붙인 N개의 병에 키위 주스를 넣었습니다. 이 때 i번째의 병의 용량은 capacities[i] 리터이며 타로가 i번째 병에 넣은 키위 주스의 양을 bottles[i] 리터라고 합니다.  
타로는 병에 키위 주스를 재분배하려고 하며, 0부터 M-1까지 M회 조작합니다. i번째의 조작은 타로가 병 fromId[i]부터 병 toId[i]에 키위 주스를 넣는 것을 의미합니다. 병 fromId[i]가 비어있거나 병 toId[i]가 꽉 차 있는 순간, 타로는 더 이상 키위 주스를 넣지 않습니다.  
N개의 요소를 가진 정수 배열 int[]를 리턴해주세요. 배열의 i번째 요소는 모든 주스를 쏟는 작업이 완료되고 i번째 병에 남아 있는 키위 주스의 양입니다.
<br/>
**Example:**

```js
1. capacities = [20, 20]
bottles = [5, 8]
fromId = [0]
toId = [1]

Returns: [0, 13]

2. capacities = [10, 10]
bottles = [5, 8]
fromId = [0]
toId = [1]

Returns: [3, 10]

3. capacities = [30, 20, 10]
bottles = [10, 5, 5]
fromId = [0, 1, 2]
toId = [1, 2, 0]

Returns: [10, 10, 0]

4. capacities = [14, 35, 86, 58, 25, 62]
bottles = [6, 34, 27, 38, 9, 60]
fromId = [1, 2, 4, 5, 3, 3, 1, 0]
toId = [0, 1, 2, 4, 2, 5, 3, 1]

Retruns: [0, 14, 65, 35, 25, 35]

5. capacities = [700000, 800000, 900000, 1000000]
bottles = [478478, 478478, 478478, 478478]
fromId = [2, 3, 2, 0, 1]
toId = [0, 1, 1, 3, 2]

Returns: [0, 156956, 900000, 856956]
```

**문제접근**

1. 키위주스를 0 ~ (N-1)번 병에 붓는다.
2. i번째 병의 용량은 capacities[i].
3. i번째 주스 양은 bottles[i].
4. fromId[i]병에서 toId[i]병으로 붓는다.
5. fromId[i]병이 비거나 toId[i]가 꽉차면 붓는 행동을 멈춘다.
6. return 값은 각각 i번째 병에 남은 주스 양의 배열이다.

결과는 두 가지로 나온다.<br/>  
(1) 주스를 모두 옮겼는데 넘치지 않고 전부 들어간 경우  
Example1의 경우. 옮길 주스의 양(fromId[i])이 기존 주스병의 남은 양(toId[i])와 같거나 작을 때
(2) 주스를 모두 옮겼는데 넘치는 경우  
Example2의 경우. 옮길 주스의 양(fromId[i])이 기존 주스병의 남은 양(toId[i]) 보다 클 때

**소스코드**

```js
const Solution = {
  solve: function(capacities, bottles, fromId, toId) {
    for (let i = 0; i < fromId.length; i++) {
      // 병 개수만큼 반복
      let result = this.pour(
        bottles[fromId[i]],
        bottles[toId[i]],
        capacities[toId[i]]
      );
      bottles[fromId[i]] = result[0];
      bottles[toId[i]] = result[1];
    }
    return bottles;
  },
  pour: function(fromAmount, toAmount, toCapacity) {
    // fromId[i]와 toId[i]를 더한 값이 capacities[i]보다 작거나 같으면 fromId[i]를 0으로 바꾸고 toId[i]를 그 합으로 한다.
    return fromAmount + toAmount <= toCapacity
      ? [0, fromAmount + toAmount]
      : [fromAmount + toAmount - toCapacity, toCapacity];
    // fromId[i] + toId[i]가 capacities[i]보다 크면 fromId[i]는 합에서 capacities[i]를 빼고 capacities[i]는 용량만큼 차 있기 때문에 용량을 toId[i]값으로 한다.
  }
};
```
