---
title: "#04. Array Cardio Day1"
category: Javascript30
---

## 공부
### 1. Array.prototype.filter()
> Q. 1500년대에 태어난 사람 필터링하기 

배열(`inventors`)의 요소들(`inventor`)을 하나씩 순회하면서, 조건과 일치하면 새롭게 필터링 되는 배열의 요소로 추가한다.(`return true`)    
`false`를 반환하는 경우 즉, 조건과 일치하지 않는 경우는 굳이 `else`절로 작성할 필요 없다. 

```javascript
const fifteen = inventors.filter(function(inventor){
    if(inventor.year >= 1500 && inventor.year < 1600){
        return true; // keep it!
    }
});
```

위의 코드를 화살표 함수로 간단히 바꾸면 아래와 같다.   
```javascript
const fifteen = inventors.filter(inventor => inventor.year >= 1500 && inventor.year < 1600 );
```
 



### 2. Array.prototype.map()
> Q. 성과 이름만 갖고 있는 배열  

`map()`은 항상 원본 배열의 길이와 똑같은, 새로운 배열을 만들어 반환한다. 

```javascript
const fullNames = inventors.map(inventor => inventor.first + ' ' + inventor.last);

// 백틱을 이용해 공백처리하기
inventors.map(inventor => `${inventor.first} ${inventor.last}`);
```




### 3. Array.prototype.sort()
> Q1. 나이가 많은 순에서 적은 순으로 정렬하기

`sort()`는 버블정렬과 같이 두 개의 요소를 비교해 정렬한다.    
1을 리턴(조건과 일치)하면 두 요소의 위치를 교환하고, -1을 리턴하면 교환하지 않는다. 

```javascript   
// if문을 삼항 연산자(ternary operator)를 이용해 한 줄로 단축
const ordered = inventors.sort((a, b) => a.year > b.year ? 1 : -1);
```


> Q2. 오래 산 순으로 정렬하기
```javascript  
const oldest = inventors.sort(function(a, b) {
    const lastGuy = a.passed - a.year;
    const nextGuy = b.passed - b.year;
    return lastGuy > nextGuy ? -1 : 1;
});
```


> Q3. 이름을 알파벳순으로 정렬하기 
`split`메소드로 lastName과 firstName을 분리시킨 후 대괄호에 선언해준 변수 `[변수1, 변수2]`에 바로 할당한다.  

```javascript  
const alpha = people.sort((lastOne, nextOne) => {
    // const parts = lastOne.split(', ');  // Array(2) ['lastName', 'firstName']
    
    // 위처럼 Array 형식이 아니라 각각 변수에 담기 위해
    // [](square bracket) 안에 변수를 선언해줌 
    const [aLast, aFirst] = lastOne.split(', ');
    const [bLast, bFirst] = nextOne.split(', ');
    return aLast > bLast ? 1 : -1;
});
```




### 4. Array.prototype.reduce()
> Q1. inventor들의 살아온 기간 총합 구하기

`reduce()` 는 for문을 돌면서 sum을 구하는 예전 방식의 코드에서 벗어날 수 있게 해준다.      
객체 배열의 값 합산시 반드시 초기값을 주어 각 항목이 reducer함수를 거치도록 해야한다. 

```javascript  
// 합계를 구하던 기존 방식
var sum = 0;
for(var i=0; i<inventors.length; i++){
    sum += inventors[i].passed - inventors[i].year;
}

// reduce를 이용한 방식
// total이 누적 합산되어 최종적으로 반환될 값이다. 
const totalYears = inventors.reduce((total, inventor) => {
    return total + (inventor.passed - inventor.year);
}, 0);
```



> Q2. 각 요소들의 합 구하기

```javascript
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];

const transportation = data.reduce(function(obj, item){
    //obj에 item과 동일한 프로퍼티가 없다면 0으로 초기화
    if(!obj[item]){
    obj[item] = 0;
    }

    obj[item]++;
    return obj;
}, {});
```

reduce메소드의 초기값을 빈 객체`{}`로 주는 것은 아래처럼 일일이  하드코딩하는 것과 같다. 
```javascript
const transportation = data.reduce(function(obj, item){
    ...
}, {
    car: 0,
    truck: 0,
    bike: 0,
    ...
});
```





### 5. NodeList -> Array
`querySelectorAll()`은 유사배열인 `NodeList`를 반환하기 때문에 배열의 모든 메소드를 사용하려면 `Array`로 변환이 필요하다. 

```javascript
// NodeList를 Array로 변환한다. 
const links = Array.from(category.querySelectorAll('a')); 

// links배열에서 text만 가진 새로운 배열을 뽑아내고, 'de'가 포함된 요소만 필터링한다. 
const de = links
            .map(link => link.textContent)
            .filter(streetName => streetName.includes('de'));
```







## 정리 
1. 분명 얼마 전에 정리했던 배열 메소드들인데... 낯설다.. 