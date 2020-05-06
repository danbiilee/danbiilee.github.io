---
title: "#08. Fun with HTML5 Canvas"
category: Javascript30
---

## 공부
### HTML5 Canvas
`canvas`요소는 `getContext()` 메서드를 이용해 렌더링 컨텍스트와 그리기 함수들을 사용할 수 있다. getContext() 메서드는 렌더링 컨텍스트 타입을 지정하는 하나의 파라미터를 갖는다. 

```javascript
const canvas = document.querySelector('#draw');
const ctx = canvas.getContext('2d');
```
