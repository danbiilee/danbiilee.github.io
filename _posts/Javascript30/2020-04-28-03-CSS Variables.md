---
title: "#03. Playing with CSS Variables and JS"
category: Javascript30
---

## 새롭게 알게 된 것들 
### 1. input:color
`type="color"`인 `input`태그가 있다는 걸 처음 알았다. 신기방기쓰.



### 2. CSS의 변수
CSS에서도 변수를 선언하고 사용할 수 있다.      
자신의 부모 요소에 선언된 변수에만 접근할 수 있기 때문에 보통 최상위 요소를 뜻하는 `:root` 가상 선택자를 이용해 변수를 선언한다. 
   

#### 2.1 :root 가상 선택자
HTML에서 최상위 요소는 html태그를 의미한다. html 태그 이름을 선택자로 쓰면 우선 순위에 1점이 부여되지만, 가상 선택자는 class로 간주되어 10점이 부여되므로 굳이 `:root` 가상 선택자를 사용하는 거라고 생각하면 된다. 

#### 2.2 변수의 선언과 사용
**변수 선언 방법**
`--변수명`    

**변수 사용법**
- 변수값이 유효한 경우: `var(변수)` 
- 변수값이 유요하지 않은 경우
    - 기본값으로 설정: `var(변수, 기본값)`
    - 다른 변수를 적용: `var(변수1, var(변수2), 기본값)`  

```css
:root {
    --base: #ffc600;
    --spacing: 10px;
    --blur: 10px;
}

img{
    padding: var(--spacing);
    background: var(--base);
    filter: blur(var(--blur));
}
```
크로스 브라우징을 위해 방어코드를 작성하자.    
```css
img{
    padding: 10px;
    padding: var(--spacing);
}
```

### 4. blur(radius)
CSS 함수 `blur()`는 주어진 이미지에 가우시안 블러를 적용한다. 


### 5. HTMLElement.dataset
`dataset`은  모든 `data-*` 속성에 대한 값을 갖고 있는 `DOMStringMap` 을 반환한다. 

```html
<input type="range" name="spacing" id="spacing" data-sizing="px">
```
위의 input 요소에 `data-sizing`이라는 사용자 지정 속성을 부여해주고, 아래의 방법으로 그 값을 읽어준다. 

```javascript
const input = document.querySelector('#spacing');

// element.dataset.keyName
console.log(input.dataset.sizing); // 'px' 
```


### 6. Document.documentElement
이 읽기 전용 속성은 문서의 루트 요소를 나타내는 요소를 반환한다. HTML문서의 경우 `html`요소를 반환한다. 


### 7. style.setProperty(propertyName, value, priority)
요소의 style 속성을 설정하는 메소드이다. 
아래 코드는  `html`요소 즉, 앞서 가상 선택자 `:root`에 선언했던 CSS 변수의 값을 재설정하는 코드이다.   

```javascript
document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
```


### 8. 이벤트
- `change` 이벤트는 input요소를 클릭했다가 떼는 순간에 이벤트가 발생한다. 
- `mousemove` 이벤트는 마우스 클릭과 관계없이 마우스 움직임 대로 이벤트가 발생한다. 



## 정리
1. input요소를 모두 선택해 이벤트 리스너의 콜백 함수로 `:root`의 속성 즉, 변수들의 값을 변경하는 `handleUpdate` 함수를 호출한다. 
