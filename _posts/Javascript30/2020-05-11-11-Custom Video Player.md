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
/* 그럼 아래는 flex-item에 width: 100% 하려는 거!?  */
.progress{ 
	flex-basis: 100%;
}
```

#### 1.5 cursor: ew-resize
해당 요소에 마우스 호버하면 커서가 좌우 화살표(?)로 바뀐다.



### 2. JS
#### 2.1 video 태그의 이벤트
- play
- pause
  
영상이 정지 상태면 `play()` 메서드를, 재생 상태면 `pause()` 메서드를 실행한다. 

```javascript
const method = video.paused ? 'play' : 'pause';
video[method](); // video.play() 혹은 video.pause()
```

`play()` 메서드가 실행되면 영상에 `play` 이벤트가 발생하고, `pause()` 메서드가 실행되면 `pause` 이벤트가 발생한다.   


- timeupdate

비디오의 재생 위치가 변경될 때 `timeupdate` 이벤트가 발생한다. 



#### 2.2 문법!? 
`mousedown`이 참인 경우에 `scrub` 함수를 실행한다.   

```javascript
progress.addEventListener('mousemove', (e) => mousedown && scrub(e)); 
```





## 정리
1. 비디오 혹은 플레이 버튼을 클릭하면 `togglePlay` 콜백함수가 호출되어 영상이 재생/정지 되고, 재생/정지될 때마다 `updateButton` 콜백함수에 의해 플레이버튼의 아이콘이 변경된다. 
2. 비디오의 재생 위치가 변경될 때 `timeupdate` 이벤트가 발생, `handleProgress` 콜백함수를 호출하여 재생바의 너비를 %기준으로 현재 영상의 위치만큼 조절한다. 
3. 스킵버튼을 클릭하면 `skip` 콜백함수가 호출되어 영상의 재생위치가 변경된다. 
	- DOM에서 스킵버튼에 `data-skip` 속성을 지정한 후 스크립트에서 `dataset.skip`으로 skip data를 핸들링한다. 
4. 재생바로 영상의 위치를 변경하는 경우 재생바를 클릭하거나 flag변수를 이용해 `mousedown`이 `true`인 경우에만 `srub` 콜백함수를 실행해 재생바의 크기만큼 영상의 재생시간을 변경한다.
