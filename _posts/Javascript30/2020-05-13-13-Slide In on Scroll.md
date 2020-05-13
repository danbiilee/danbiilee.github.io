---
title: "#13. Slide In on Scroll"
category: Javascript30
---


## 공부
### 1. CSS
#### 1.1 text-align
- justify: 양쪽 정렬



### 2. JS
#### 2.1 setTimeout()



#### 2.2 offsetTop / height / innerHeight / outerHeight / scrollY
slideInAt변수는 스크롤을 이미지 높이 반 쯤까지 위치시켰을 때 브라우저 맨 위부터 스크롤 위치까지의 높이를 담는다. 즉, 이미지가 보여지는 애니메이션이 발생할 지점을 뜻한다.    
- `window.scrollY`: 브라우저 맨 위에서부터 스크롤을 내린 지점까지의 높이이다.
- `window.innerHeigh`: 실제로 보여지는 화면의 높이로 화면의 사이즈가 변경되면 같이 변경된다.     
  
스크롤을 내리다가 slideInAt변수의 높이에 다다르면 즉, 브라우저 맨 위에서부터 스크롤이 특정 이미지의 높이의 반까지 위치하게 되면 애니메이션 효과가 나타나게 될 것이다. 

```javascript
const slideInAt = (window.scrollY + window.innerHeight) - sliderImages.height / 2;
```

imageBottom변수는 스크롤을 아래에서 위로 올릴 때 똑같은 애니메이션 효과를 주기 위해 브라우저 맨 위부터 스크롤이 올라갈 때 보여질 이미지의 밑변 기준까지의 높이를 구한 것이다.
- `sliderImage.offsetTop`: 브라우저의 맨 위에서부터 해당 이미지 윗변까지의 높이이다. 즉 브라우저 맨 위에서 이미지가 얼마나 떨어져있는지를 의미한다.

`sliderImage.offsetTop`에 이미지 높이를 더하면 브라우저 맨 위부터 이미지의 밑변까지의 높이이다.  

```javascript
const imageBottom = sliderImage.offsetTop + sliderImage.height;
```


그리고 아래와 같이 이미지가 반이 보이고 있는지, 스크롤이 위로 올라가고 있는 지를 확인할 수 있는 변수를 셋팅한다.
```javascript
// [브라우저~이미지 윗변] 높이보다 slideInAt이 크다는 건 이미지가 반이 보이고 있다는 의미!
const isHalfShown = slideInAt > sliderImage.offsetTop;

// 스크롤한 높이가 [브라우저~이미지 밑변] 높이보다 작아졌다면 스크롤이 올라가고 있는 것. 즉, 이미지가 다시 보이기 시작했다는 의미!
const isNotScrolledPast = window.scrollY < imageBottom; 
```

두 변수가 모두 참이라면 이미지가 보이는 애니메이션을 활성화할 수 있도록 클래스를 추가한다. 





#### 2.3 debounce 와 throttle
`debounce` 와 `throttle`은 과다한 이벤트의 반복 실행을 방지하는 역할을 한다.  
- `dobounce`: 이벤트를 하나로 그룹화 하여 특정 시간이 지난 후에 호출될 수 있도록 구조화하는 것이다. 즉, 동일한 이벤트가 반복되어 발생하는 경우 마지막 이벤트가 발생하고 일정 시간동안 해당 이벤트가 다시 발생하지 않으면(이벤트의 반복이 끝난 것 같으면), 해당 이벤트의 콜백함수를 실행한다.
- `throttle`: 동일한 이벤트가 반복적으로 실행되는 경우 이벤트의 실제 반복주기과 상관없이 임의로 설정한 일정 간격으로 콜백함수가 실행된다. 

> 대표적으로 Lodash 라는 라이브러리에서 이 기능을 제공한다.


아래는 `scroll` 이벤트가 발생할 때마다 매번 `checkSlide` 콜백 함수를 실행하는 게 아니라, `debounce` 함수의 두 번째 인자로 준 시간(기본값 20 milliseconds)마다 실행하도록 하는 코드이다. 
```javascript
function debounce(func, wait = 20, immediate = true){
	// ...
}
window.addEventListener('scroll', debounce(checkSlide));
```






## 정리
1. 이미지가 반이 보이고 있는지, 아니면 스크롤이 다시 위로 올라가고 있는지를 판단해서 두 경우에만 `active` 클래스를 더해, 이미지가 나타나는 애니메이션 효과가 나타나도록 한다. 
2. `debounce` 함수를 이용해 스크롤 이벤트가 발생할 때 최소한으로만 `checkSlide` 함수가 실행되도록 한다. 
