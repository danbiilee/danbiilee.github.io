---
title: "#15. LocalStorage"
category: Javascript30
---

## 공부
### 1. HTML / CSS
#### 1.1 svg 태그 
`SVG`는 `Scalable Vector Graphics`의 약자로 2차원의 벡터 이미지를 만들기 위한 태그이며 XML기반이다.   
SVG의 장점으로는 기기들의 비율에 대응하기 위해 필요한 원본X2 사이즈의 이미지가 따로 필요하지 않다는 점과 CSS를 이용해 스타일링이 가능하고, JS를 이용해 이벤트 핸들링이 가능하다는 점등이 있다. 


#### 1.2 + 선택자 
인접 선택자로 앞의 요소 바로 뒤에 있는 요소만 선택한다. 

```css
/* 앞의 input태그 바로 다음의 label태그만 선택 */
.plates input + label
```

#### 1.3 content 속성 
`content`속성은 `:before`나 `:after`라는 가상 클래스를 사용해 요소의 전후에 텍스트나 이미지들의 콘텐츠를 삽입할 때 사용한다. HTML문서에 포함되지 않은 요소를 CSS에 의해 새롭게 생성해주는 가상의 요소이다.    
> ::before, ::after는 CSS3의 문법!

```css
.plates input + label:before {
	content: "⬜️";
}
```


### 2. JS
#### 2.1 reset()
`reset()` 메소드는 form태그 안의 input태그들의 value값을 초기화시킨다. 하지만 	타입이 `hidden`, `checkbox`, `radio`인 요소에 대해서는 초기화를 시켜주지 않으므로 주의할 것. 



### 3. localStorage
HTML5에서 제공하는 클라이언트 저장소 기능으로는 `localStorage`와 `sessionStorage`가 있다.   
두 가지는 세션에 따라 데이터가 유지되는지 여부에 따라 구분할 수 있고, `sessionStorage`의 경우에만 세션이 종료되면 저장된 데이터도 함께 사라진다. 
- setItem(key, value): key값으로 데이터를 등록한다.
- getItem(key): key값으로 데이터를 불러온다. 파라미터를 전달하지 않으면 저장소에 담겨 있는 모든 정보를 불러온다. 
- removeItem(key): 특정 key값의 데이터를 삭제한다.
- clear(): 저장소의 모든 정보를 삭제한다. 



## 정리 
1. 