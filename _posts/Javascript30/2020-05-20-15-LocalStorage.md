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
#### 2.1 e.preventDefault()
이벤트의 고유 동작을 중단시키는 메소드이다. 
여기서는 데이터 저장을 서버단이 아닌 클라이언트단에서 처리하기 때문에 form이 `submit`될 때 해당 메소드를 적용시키면 페이지가 제출되는 것을 막을 수 있다. 
> e.stopPropagation()
> 이벤트가 부모 요소에게 전달되지 않게 막아주는 메소드이다. 

```javascript
const addItems = document.querySelector('.add-items'); // form요소

function addItem(e){
	e.preventDefault(); 

	// this = form태그 
	const text = (this.querySelector('[name=item')).value;
}

addItems.addEventListener('submit', addItem);
```

위의 코드에서 하나 더 살펴보면, input 요소를 찾을 때, `document`에서부터 찾을 수도 있지만 해당 함수 안에서 `this`가 form 요소이기 때문에 바로 `this`에서부터 범위를 좁혀 요소를 찾을 수 있다. 특히 한 페이지에 form 요소가 여러 개 있을 때 이 방법을 쓰면 유용하다. 

#### 2.2 reset()
`reset()` 메소드는 form요소 안의 value값들을 초기화시킨다. 하지만 타입이 `hidden`, `checkbox`, `radio`인 요소에 대해서는 초기화를 시켜주지 않으므로 주의할 것. 


#### 2.3 matches()
선택한 요소 중에서 전달받은 선택자에 해당하는 요소가 하나라도 존재하면 `true`를 반환하고, 하나도 없다면  `false`를 반환한다.   
> 제이쿼리의 `is()` 메소드와 동일하다. 

```javascript
// e.target에 input 요소가 없다면 return한다. 
if(!e.target.matches('input')) return;
```



### 3. localStorage
HTML5에서 제공하는 클라이언트 저장소 기능으로는 `localStorage`와 `sessionStorage`가 있다.   
두 가지는 세션에 따라 데이터가 유지되는지 여부에 따라 구분할 수 있고, `sessionStorage`의 경우에만 세션이 종료되면 저장된 데이터도 함께 사라진다. 

- setItem(key, value): key값으로 데이터를 등록한다. value값으로는 항상 문자열을 전달해야 한다. 

```javascript
console.log(items.toString()); // '[object Object]'

//toString()가 아니라 JSON.stringify()를 이용해 배열을 문자열로 변환해줘야한다. 
localStorage.setItem('items', JSON.stringify(items)); 
```

- getItem(key): key값으로 데이터를 불러온다. 파라미터를 전달하지 않으면 저장소에 담겨 있는 모든 정보를 불러온다.

```javascript
// localStorage에 items를 키로 하는 값이 있다면 그 문자열을 객체로 변환하여 반환한다. (값이 없다면 빈 배열)
const items = JSON.parse(localStorage.getItem('items')) || [];

// 페이지가 로딩될 때마다 리스트를 업데이트한다.
populateList(items, itemsList);
```

- removeItem(key): 특정 key값의 데이터를 삭제한다.
- clear(): 저장소의 모든 정보를 삭제한다. 




### 4. 이벤트 위임(Event Delegatioon)
이번 예제에서 자식 요소인 input+label태그 즉, 리스트들은 동적으로 추가되는 요소이므로 직접 `click` 이벤트 리스너를 더하면 원하는 대로 작동하지 않는다. 
이럴 때는 자식 요소가 아닌 모든 리스트를 포함하는 부모 요소인 ul태그에 이벤트 리스너를 더해준다. 그러면 자식 요소에(HTML에 존재하고 있는 자식 요소든 동적으로 추가될 자식 요소든) `click` 이벤트가 발생할 때 부모 요소가 직접 이벤트를 제어하지 않고 자식요소에게 이벤트를 전달해준다. 

```javascript
function toggleDone(e){
	// 부모 요소에 이벤트가 발생했지만 클릭한 대상이 그 중 이벤트를 전달하고 싶은 자식 요소인지를 확인하는 조건을 걸어 이벤트를 전달한다. 
	if(!e.target.matches('input')) return;
}

// itemsList = ul태그
itemsList.addEventListener('click', toggleDone);
```



## 정리 
1. 더하기 버튼을 클릭하면 `items` 배열에 입력한 `item`을 추가하고, `localStorage`에 저장 후 `populateList` 함수를 통해 리스트화면을 리렌더한다. 
2. `populateList` 함수는 배열과 리스트가 덤프될 html요소를 인자로 받는다. `items` 배열을 루프로 순회하면서 `item` 의 정보를 담은 li 태그를 리턴하고, html에 덤프한다. 
   - `item` 하나가 추가될 때마다 `itemsList`의 전체가 변경되기 때문에 성능상 이슈 생길 수 있다. 리액트나 앵귤러를 이용해서 최소한의 부분만 변경할 수 있는 방법 찾아보기!
3. 체크박스를 클릭하면 **(체크박스를 포함하는 부모요소를 클릭하면(이벤트 위임 발생))** 해당 `item`의 done(체크여부) 속성값을 그 반대로 변경하고(체크 -> 체크해제 / 체크해제 -> 체크), `localStorage`에 변경된 값을 재저장 후 `populateList` 함수를 통해 리스트화면을 리렌더한다. 
4. 이벤트가 발생하지 않아도 페이지가 로딩될 때마다 리스트 화면이 리렌더될 수 있도록 script의 전역에 `populateList`함수를 호출한다. 