---
title: "#07. Array Cardio Day2"
category: Javascript30
---

## 공부
### 1. Array.prototype.some()
배열의 각 요소에 대해 `callback`함수를 실행해 참을 반환하는 요소를 찾으면 `some`메소드는 그 즉시 `true`를 반환, 모든 값에서 거짓을 반환하면 `false`를 반환한다.
- 빈 배열에서 호출하면 무조건 `false`를 반환한다. 


### 2. Array.prototype.every()
`some`메소드와 반대로 `callback`함수가 거짓을 반환하는 요소를 발견한 경우 `every`메소드는 즉시 `false`를 반환, 모든 값에서 참을 반환하면 `true`를 반환한다. 
- 빈 배열에서 호출하면 무조건 `true`를 반환한다. 



### 3. 배열의 요소 삭제하기
`findIndex`메소드로 특정 `index`를 구하고, `spread syntax`(전개구문)과 `slice`메소드를 이용해 원본 배열의 변경없이 해당 요소만 삭제된 새 배열을 만든다. 

```javascript
const newComments = [
    ...comments.slice(0, index), 
    ...comments.slice(index+1)
];
```

cf) `splice`메소드는 원본 배열을 변경한다. 



