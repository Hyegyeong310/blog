---
layout: post
title: '[JS-Basic] Recursive Function'
author: HyeGyeong
categories: [JS-Basic]
image: 'assets/images/8.jpeg'
---

# Recursive Function

## 1. Recursive Function이란?

한국어로 '재귀함수'라 한다. 어느 함수가 있을 때 그 함수가 자기 자신을 다시 부르는 함수를 뜻한다.<br>
재귀함수는 제한을 걸지 않으면 무한 루프로 돌 수 있다. 밑의 예시처럼 제한을 걸어야 한다.<br>
그리고 재귀함수가 실행될 때 마다 그 함수는 반드시 초기 상태로 되돌아가도록 만들어져야 한다.

<img src = "https://wayhome25.github.io/assets/post-img/cs/sum.png"><br>

> (출처: 초보몽키의 개발공부로그)
> <img src="http://kstatic.inven.co.kr/upload/2018/05/08/bbs/i14088991378.png">
> (출처: 인벤 유머게시판: 무한루프의 예)

## 2. Resursive Function 예시 (Factorial)

### 2.1 factorial 구현 (재귀함수 X)

```javascript
function factorial(num) {
  var result = 1;
  for (var i = 1; i <= num; i++) {
    result *= i;
  }
  return result;
}
```

### 2.2 factorial 구현 (재귀함수 O)

```javascript
function factorial(num) {
  var endNum = 1;
  if (num < 0) {
    return -1;
  } else if (num === 0) {
    return 0;
  }
  if (num === endNum) {
    // 제한. num가 1과 같으면 1을 리턴한다.
    return endNum;
  } else {
    return num * factorial(num - 1);
  }
}
```

factorial(5) // 120 를 예시로
return num \* factorial(num-1)을 풀어보면<br>

```javascript
return 5 * factorial(4)<br>
           return 4 * factorial(3)<br>
                      return 3 * factorial(2)<br>
                                 return 2 * factorial(1)<br>
                                            return 1; // endNum
```
