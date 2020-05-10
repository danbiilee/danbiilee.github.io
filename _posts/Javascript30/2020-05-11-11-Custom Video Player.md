---
title: "#11. Custom Video Player"
category: Javascript30
---

## 공부
### 1. CSS 
#### 1.1 :fullscreen
fullscreen일 때만 적용되는 CSS 가상 클래스. 

```css
.player:fullscreen{ ... }
.player:-webkit-full-screen{ ... }
```

#### 1.2 flex-wrap
`flex-wrap` 속성은 flex-item 요소들을 강제로 한 줄에 배치할 건지, 아니면 영역 내에서 벗어나지 않고 여러 행으로 나누어 배치할 건지 설정하는 속성이다. 
- nowrap: 기본값으로 flex-item 요소들이 flex-container 영역을 벗어나도 한 줄에 배치한다. 시작점은 `flex-direction`에 의해 결정된 방향으로 적용된다.
- wrap: flex-item 요소들이 여러 행에 걸쳐 배치된다. 일반적으로 위에서 아래로 쌓인다.
- wrap-reverse: `wrap` 속성값과 동일하지만, 요소가 나열되는 시작점과 끝점의 기준이 반대로 배치된다. 


#### 1.3 flex-basis
`flex-basis` 속성은 flex-item의 초기 크기를 정한다. `box-sizing`을 따로 지정하지 않는다면 콘텐츠 박스의 크기를 변경한다.   
`auto`값이 아닌 `flex-basis`속성과 `width`(`flex-direction: column`인 경우 `height`)값을 동시에 적용한 경우 `flex-basis`속성이 우선 적용된다. 

```css
/* 그럼 아래는 flex-item에 width: 100% 하려는 의도!?  */
.progress{ 
	flex-basis: 100%;
}
```

#### 1.5 cursor: ew-resize
해당 요소에 마우스 호버하면 커서가 좌우 화살표(?)로 바뀐다.



### 2. JS
#### 2.1 video 태그 다루기
영상이 정지 상태면 `play()` 메서드를, 재생 상태면 `pause()` 메서드를 실행한다. 

```javascript
const method = video.paused ? 'play' : 'pause';
video[method](); // video.play() 혹은 video.pause()
```

`play()` 메서드가 실행되면 영상에 `play` 이벤트가 발생하고, `pause()` 메서드가 실행되면 `pause` 이벤트가 발생한다. 