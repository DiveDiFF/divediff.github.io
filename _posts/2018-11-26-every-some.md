---
title: "every, some method in Array"
date: 2018-11-26 16:48:20 -0400
categories: React Array javaScirpt
comments: true
---

# javaScirpt every, some method in Array

지금까지 javaScirpt에서 Array를 많이 다루지만, 사실 사용하는 method는 foreach, map, find, filter 정도.

validate 체크와 같이 특정 조건을 모두 통과 시키는지를 깔끔하게 코딩하는데 유용한 method 두개를 배웠다.

some, every

```javascript
function isBiggerThan10(element, index, array) {
  return element > 10;
}
[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true
```

> 배열 요소 중 하나라도 10보다 크면 true

<br><br>

every는 모든 요소가 다 조건을 충족해야만 true를 반환한다.

이를 validate 체크에 응용하면

```javascript

validate () {
  return Array.from(['name', 'phone']).every(ref => this[ref].validate())
}

handleSubmit () {

  if (validate()) {
    ...
  }
...
}

```

> 한줄로 끝.. 각각의 validate 결과가 모두 true인 경우만 true를 반환함.

<br><br>

기존에 반복문을 돌려 배열을 탐색하는 방식보다 훨씬 깔끔...
