---
title: "#17. Sort Without Articles"
category: Javascript30
---

## 공부
### 1. Array.prototype.sort()
`sort()` 메소드의 파라미터로 정렬순서를 정의하는 `compareFunction`을 전달할 수 있다.     
`compareFunction(a,b)`의 리턴값이 0보다 작으면 a가 앞으로, 0보다 크면 b가 앞으로 정렬되고, 0이면 정렬순서는 변경되지 않는다. 

```javascript
arr.sort((a, b) => {
    // a가 b보다 작으면 a가 앞에 정렬, 
    // a가 b보다 크면(b가 a보다 작으면) b가 앞에 정렬된다
    return a < b ? -1 : 1;
});
```




