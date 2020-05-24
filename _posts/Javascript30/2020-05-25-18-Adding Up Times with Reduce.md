---
title: "#18. Adding Up Times With Reduce"
category: Javascript30
---

## 공부
### 1. parseFloat()
`parseFloat()` 함수는 문자열을 분석해 부동소수점 실수로 반환한다. 

```javascript
// .map(parseFloat)의 문법이 어떻게 되는 거지?! 
const [mins, secs] = timeCode.split(':').map(parseFloat);
```


## 정리
`data-time`으로 담겨있는 비디오의 시간들을 `reduce()`메서드를 이용해 초단위로 전부 더하고, 다시 시/분/초로 계산한다. 


