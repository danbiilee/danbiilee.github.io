---
title: "#22. Follow Along Link Highlighter"
category: Javascript30
---


## 공부
### 1. getBoundingClientRect()
요소의 상대위치를 구하는 메소드이다. 


## 정리 
1. 동적으로 하이라이트 요소를 생성 후 body 태그의 자식으로 추가해둔다.
2. a 태그에 `mouseenter` 이벤트가 발생할 때 `highlightLink` 콜백함수를 실행한다. 
3. `highlightLink`: 이벤트 리스너가 더해진 a 태그의 상대적인 너비, 높이, 뷰포트로부터의 좌표값을 구해서 동적으로 하이라이트 요소의 style을 설정해준다. 그럼 a 태그에 호버할 때 그 크기, 위치에 맞게 하이라이트가 짠! 하구 나타난다. 
- a 태그에 호버하지 않으면 하이라이트 요소는 높이와 너비가 0이므로 화면상에서는 보이지 않는다.
- 화면을 스크롤하면 스크롤한 거리만큼 하이라이트 요소가 따라오지(?) 못한다. 방법은 여러가지가 있겠지만 `window.scrollY`를 더해 간단히 해결해 줄 수 있다.

```javascript
const linkCoords = this.getBoundingClientRect();

highlight.style.transform = `translate(${linkCoords.top + window.scrollY}px, ${linkCoords.left + window.scrollX}px)`;
```
