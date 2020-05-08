---
title: "#09. Dev Tools Domination"
category: Javascript30
---

## 공부
### 1. console.log() 문자열 치환
`log()` 메서드처럼 문자열을 받는 콘솔 메서드에는 치환 문자열을 사용할 수 있다. 
- %o 또는 %O : 자바스크립트 객체를 출력한다.
- %d 또는 %i : 정수를 출력한다.
- %f : 부동소수점 수를 출력한다. 
- %s : 문자열을 출력한다. 
- %c : 콘솔 출력에 CSS스타일을 적용한다. 

```javascript
console.log('I am a %s!', 'string'); // I am a string!

console.log('%c log text', 'font-size:50px; background:red;');
```

문자열의 경우 템플릿 리터럴이 제공하는 문자열 인터폴레이션 기능을 사용해도 된다. 문자열 인터폴레이션은 `${ }`으로 표현식을 감싸는 방식으로, 표현식은 문자열로 강제 형변환된다.   
```javascript
const first = 'Ung-mo';
const last = 'Lee';
console.log(`My name is ${first} ${last}.`); // My name is Ung-mo Lee.
```


### 2. console.assert()
첫 번째 매개변수가 `false`인 경우 메시지와 스택 추적을 출력한다.



### 3. console.groupCollapsed(), groupEnd()
- group(), groupCollapsed(): 새로운 인라인 그룹을 생성해, 이후 모든 출력을 한 단계 들여쓴다. `groupCollapsed()` 메서드는 `group()` 메서드와 달리 그룹이 접혀있는 상태로 출력된다. 
- groupEnd(): 현재 인라인 그룹을 나온다.



### 4. console.time(), timeEnd()
- time(): 주어진 이름의 타이머를 실행한다. 
- timeEnd(): 실행시킨 타이머를 멈추고, 소요시간을 출력한다.

```javascript   
console.time('timer test');
//... Code
console.timeEnd('timer test'); // timer test: 100.001ms
```


### 5. 그 외 console의 메서드들
- dir(): 주어진 자바스크립트 객체의 속성 목록을 펼쳐 살펴볼 수 있는 형태로 출력한다. 
- warn()
- error()
- info()
- table(): 표 형태의 데이터를 표에 그려 출력한다. 
- clear(): 콘솔의 내용을 지운다.
- count(): 주어진 매개변수로 메서드를 호출한 횟수를 출력한다.
- trace(): 스택 추적을 출력한다. 

