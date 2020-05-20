---
title: "#16. Mouse Move Shadow"
category: Javascript30
---


## 공부
### 1. HTML / CSS
#### 1.1 contenteditable 속성 
HTML태그의 속성으로 `contenteditable`을 지정하면 브라우저에서 해당 요소의 텍스트를 수정할 수 있게 된다.   
값은 `true` 혹은 `false`, `true`일 때는 생략이 가능하다. 

```html
<h1 contenteditable>🔥WOAH!</h1>
```


#### 1.2 display: flex가 자식 요소에게 주는 영향!? 
부모 요소에 `display: flex`를 선언하면 자식 요소는 저절로 `inline-block`화 된다.


#### 1.3 text-shadow
`text-shadow`의 값을 하나만 줄 수도 있지만, 콤마로 여러 개를 이어붙이면 하나의 요소에 여러 개의 `text-shadow`가 나타나게 된다. 

```javascript
text.style.textShadow = `
	${xWalk}px ${yWalk}px 0 rgba(255,0,255,0.7),
	${xWalk * -1}px ${yWalk}px 0 rgba(0,255,255,0.7),
	${yWalk * -1}px ${xWalk}px 0 rgba(0,255,0,0.7),
	${yWalk}px ${xWalk * -1}px 0 rgba(0,0,255,0.7)
`;
```



### 2. JS
#### 2.1 비구조화 할당
이제 조금 익숙해진 비구조화 할당 문법. 그러나 또 새로운 것을 만났다! 비구조화 할당 시 원하는 변수명을 지정해줄 수도 있나보다.  

```javascript
// hero의 offsetWidth를 width라는 변수에 할당한다.
const { offsetWidth: width, offsetHeight: height } = hero;

console.log(offsetWidth, offsetHeight); // Uncaught ReferenceError: offsetWidth is not defined
console.log(width, height); // 편-안
```