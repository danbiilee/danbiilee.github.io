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

#### 1.4 cursor: ew-resize
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




#### 2.2 동영상 풀스크린
비디오 요소의 컨테이너에 `requestFullScreen()` 을 사용한다. 

```javascript
player.requestFullscreen();
```

풀스크린을 해제할 때는 document 객체에 `exitFullScreen()`을 사용한다. 

```javascript
document.exitFullScreen();
```




#### 2.3 문법!? 
`mousedown`이 참인 경우에만 `scrub` 함수를 실행한다.   

```javascript
progress.addEventListener('mousemove', (e) => mousedown && scrub(e)); 
```



#### 2.4 querySelector
```html
<div class="player">
	<video class="viewer"></video>
</div>
```
HTML 구조가 위와 같다면 `document.querySelector()` 대신 아래와 같이 부모 요소인 player를 기준으로 자식 요소를 선택해도 된다.   

```javascript
const player = document.querySelector('.player');
const video = player.querySelector('.viewer');
```






## 정리
1. 비디오 혹은 플레이 버튼을 클릭하면 `togglePlay` 콜백함수가 호출되어 영상이 재생/정지 되고, 재생/정지될 때마다 `updateButton` 콜백함수에 의해 플레이버튼의 아이콘이 변경된다. 
   - 단순히 클릭에 의해서만 아니라 다른 방법들로 영상이 재생/정지될 수 있으므로 `updateButton` 함수는 `click` 이벤트로 묶여있는 `togglePlay` 함수와는 분리하는 것이 좋다. 
2. 비디오가 재생될 때 `timeupdate` 이벤트가 발생, 이 때 `handleProgress` 콜백함수를 호출하여 영상 시간 대비 현재 재생 위치를 %기준으로 환산해 영상의 너비를 조절한다. 

```javascript
progressBar.style.flexBasis = `${(video.currentTime / video.duration) * 100}`;
```

3. 스킵버튼을 클릭하면 `skip` 콜백함수가 호출되어 영상의 재생위치가 변경된다. 
	- DOM에서 스킵버튼에 `data-skip` 속성을 지정한 후 스크립트에서 `this.dataset.skip`으로 skip data를 핸들링한다. 
4. 재생바를 직접 움직여 영상의 재생위치를 변경할 땐 `click`과 `mousemove` 이벤트를 이용한다. `mousemove`인 경우엔 flag변수 `mousedown`이 `true`일 때만 `srub` 콜백함수를 실행한다.    
아래 코드와 같이 영상너비(`offsetWidth`) 대비 내가 클릭한 재생바의 위치(`offsetX`)만큼 비디오 영상의 시간을 구해 대입한다. 

```javascript
video.currentTime = (e.offsetX / progress.offsetWidth) * video.duration;
```
