---
title: "#22. Follow Along Nav"
category: Javascript30
---


## 공부
### 1. getBoundingClientRect()
요소의 상대위치를 구하는 메소드이다. 


## 정리 
1. 자바스크립트로 하이라이트 요소를 생성 후 body 태그의 자식으로 추가해둔다.
2. a 태그에 `mouseenter` 이벤트가 발생할 때 `highlightLink` 콜백함수를 실행한다. 
3. 이벤트 리스너가 더해진 a 태그의 상대적인 너비, 높이, 뷰포트로부터의 좌표값을 구해서 자바스크립트를 통해 동적으로 하이라이트 요소의 style을 지정해준다.  