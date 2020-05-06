---
title: "#05. Flex Panel Gallery"
category: Javascript30
---


## 공부
### 1. CSS 
#### 1.1 box-sizing: border-box
`box-sizing`은 박스의 크기를 화면에 표시하는 방식을 설정하는 속성이다.    
값을 `border-box`로 지정하면 `border`값을 포함한 크기를 지정하기 때문에 박스의 `width`, `height`값을 예측하기 더 쉬워진다.    

모든 요소에 이 값을 지정하면 아래와 같다.     
```css
html {
    box-sizing: border-box;
}
*, *:before, *:after{
    box-sizing: inherit;
}
```

#### 1.2 Flexible Box Layout
플렉스 박스(flex box)는 플렉스 컨테이너(flex container)와 플렉스 요소(flex item)로 구성된다. 플렉스 박스를 위해 제공되는 속성은 아래와 같다.   

##### 1.2.1 display 속성
HTML요소를 플렉스 컨테이너로 지정하기 위해선 `display` 속성을 설정하면 된다. 플렉스 컨테이너는 언제나 하나 이상의 플렉스 요소를 포함해야 한다.   
- flex: 블록 타입
- flex-inline: 인라인 타입


##### 1.2.2 flex-direction 속성
`flex-direction` 속성은 플렉스 컨테이너 안에서 플렉스 요소가 배치될 방향을 설정한다. 
- row: 플렉스 요소는 왼쪽에서 오른쪽으로, 위쪽에서 아래쪽으로 배치된다.(기본값)
- row-reverse: `direction` 속성값이 `ltr(left-to-right)`이면, 그 반대인 오른쪽에서 왼쪽으로 배치된다. 
- column: 수직 방향인 위쪽에서 아래쪽으로 배치된다. 
- column-reverse: 아래쪽에서 위쪽으로 배치된다. 


##### 1.2.3 justify-content 속성
`justify-content` 속성은 플렉스 요소의 수평 방향 정렬 방식을 설정한다. 
- flex-start: 기본 설정으로, 컨테이너의 앞쪽에서부터 배치된다.
- flex-end: 컨테이너의 뒤쪽에서부터 배치된다.
- center: 컨테이너의 가운데에서부터 배치된다. 
- space-between: 플렉스 요소는 요소들 사이에만 여유 공간을 두고 배치된다.
- space-around: 플렉스 요소는 앞, 뒤, 요소들 사이에도 여유 공간을 두고 배치된다.


##### 1.2.4 align-items 속성
`align-items` 속성은 플렉스 요소의 수직 방향 정렬 방식을 설정한다. 두 줄 이상을 갖는 플렉스 박스에서만 효과가 나타난다. 
- stretch: 기본 설정으로, 플렉스 요소의 높이가 컨테이너의 높이와 같에 변경된 뒤 배치된다.
- flex-start: 플렉스 요소는 컨테이너의 위쪽에 배치된다.
- flex-end: 컨테이너의 아래쪽에 배치된다.
- center: 컨테이너의 가운데에 배치된다.
- baseline: 컨테이너의 기준선(baseline)에 배치된다. 


##### 1.2.5 flex-wrap
##### 1.2.6 flex-flow
##### 1.2.7 align-content



## 정리
`flex`를 중첩해서 이용하면 `width`속성을 쓰지 않고서도 요소의 크기를 조절할 수 있다!

```css
.panels {
    display: flex; 
}
.panel {
    /* 
        1. panel들은 panels의 flex-item이면서 동시에 자식 p태그들의 flex-container가 된다.
        2. flex: 1은 컨테이너의 남는 공간을 panel들이 동일하게 분배해 가짐을 의미한다. 즉 모든 panel들이 동일한 크기를 갖게 된다. 
        3. flex-direction: column은 panel을 컨테이너로 갖는 플렉스 요소들(p태그)의 수평 정렬을 수직 정렬로 변경한다.
    */
    display: flex; 
    flex: 1;
    flex-direction: column; 
    justify-content: center; 
    align-items: center;
}

/* panel의 자식요소 p태그들(3개) */
.panel > * {
    display: flex; 
    flex: 1 0 auto; /* 요소들의 수만큼 세로로 동일한 크기를 갖게 해준다. */
    justify-content: center;
    align-items: center;
}

.panel.open {
    /* 
        open클래스가 있는 panel은 나머지 panel들보다 크기가 5배 커지게 된다. 
        여기선 생략했지만, panel에 transition속성을 설정했기 때문에 애니메이션 효과가 난다. 
    */
    flex: 5; 
    font-size: 40px;
}
```









