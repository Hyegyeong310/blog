---
layout: post
title: "[JS-Basic] Memoization"
author: HyeGyeong
category: JS-Basic
image: "assets/images/7.jpeg"
---

# Memoization

## 1. Memoization이란?

메모이제이션은 반복되는 패턴을 파악하여 그 값을 메모리에 저장했다가 다시 계산하지 않고 저장된 값을 그대로 불러오는 기법을 말한다.<br>
이미 있는 값을 구해야 할 때 다시 계산하지 않기 때문에 빨리 실행시킬 수 있다.<br>
같은 실행을 할 때 함수를 만들어서 재활용 하는 것과 같은 맥락이라 이해하면 된다.<br>
메모이제이션을 사용하기 좋은 예시로는 팩토리얼, 피보나치 수열 등이 있다.

## 2. Memoization을 이용한 Resursive Function 예시 (Factorial)

### 2.1 factorial 구현 (재귀함수만)

```javascript
var factorial2 = function(x) {
  if (x === 0) {
    return 1;
  }
  return x * factorial2(x - 1);
};
console.log(factorial2(5)); // 5 * 4 * 3 * 2 * 1 * 1 = 120
console.log(factorial2(7)); // 7 * 6 * 5 * 4 * 3 * 2 * 1 * 1 = 5040

// (factorial2(7))은 (7 * 6 * factorial2(5))과 같으나 재귀함수만 이용하면 무조건 처음부터 끝까지 계산을 한다. 필요없는 반복이 들어간다.
```

### 2.2 factorial 구현 (재귀함수 + Memoization + IIFE)

```javascript
var factorial3 = (function() {
  var save = {}; // 결과 저장 {1: 1, 2: 2, 3: 6 ...}
  var fact = function(num) {
    if (num > 0) {
      // num이 0보다 크면
      var saved = save[num - 1] ? save[num - 1] : fact(num - 1); // save에 있는 키면 그 값을 가져오고 없으면 fact 함수 실행
      var result = num * saved;
      save[num] = result; // save에 key(num), value(result) 추가
      console.log(`saved: ${saved}, result: ${result}`);
      return result;
    } else {
      return 1; // 0보다 작거나 같으면 1 리턴
    }
  };
  return fact; // fact함수 리턴 (클로져)
})();
console.log(factorial3(5)); // 5 * 4 * 3 * 2 * 1 = 120
console.log(factorial3(7)); // 7 * 6 * 120 = 5040

// factorial3(5)는 save에 '5' key가 없기 때문에 처음부터 실행한다. 실행하고 나면 save는 5,4,3,2,1 key와 값을 저장한다.
// factorial3(7)을 실행하면 5는 있기 때문에 값을 바로 가져오고 7,6에 대한 fact만 실행한다. factorial3(7) 실행이 끝나고 나면 save는 7,6 key와 value를 갖는다.
```

### 2.3 function Memoization

Lodash 라이브러리를 기반으로 한 underbar 문제에서 며칠을 잡았던 문제.<br>
콜백함수에 들어오는 인자를 key, 그 인자의 결과값을 value로 넣어서 사용하는 memoize 함수를 구현하는 문제였는데<br>
해결이 안 됐던 부분은 ([1,2,3])과 (1,2,3)을 같은 인자로 보고 2번 불러야 하는 것을 1번만 부르는 것이었다.<br>
JSON.stringify로 인자를 string화 해주고 memo 객체의 key로 넣어주니 해결...<br>

```javascript
_.memoize = function(func) {
  var memo = {};
  return (...args) => {
    var temp = JSON.stringify(args); // args를 텍스트화
    if (memo[temp]) {
      return memo[temp];
    }
    return (memo[temp] = func.apply(this, args));
  };
};
```
