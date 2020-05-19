---
title: "#14. JS Reference VS Copy"
category: Javascript30
---


## 공부
string, number, boolean(원시 데이터 타입)은 복사할 때 원본 값 자체를 할당(call-by-value)하기 때문에 복사한 쪽 값을 변경해도 원본에 영향을 주지 않는다.    
하지만 object, array(객체 데이터 타입)은 복사할 때 값이 아니라 그 값을 참조하고 있는 주소를 할당(call-by-reference)하므로 복사한 쪽 값을 변경하면 결과적으로 그 값이 가리키고 있는 주소의 원본을 변경하게 된다.  

### 1. Array 복사하기(call-by-value)
#### 1.1 array.slice()
`slice()`메소드를 파라미터 없이 호출하면 원본 배열의 변경없이 배열의 전체를 복사해 반환한다. 

```javascript
const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
const team = players.slice();
```

#### 1.2 빈 배열에 concat()
players배열의 요소들을 전부 합쳐서 빈 배열에 담는다. 

```javascript
const team2 = [].concat(players);
```

#### 1.3 ES6 Spread 문법
players배열의 모든 반복 가능한(iterable) 요소들을 새로운 빈 배열에 담는다. 

```javascript
const team3 = [...players];
```

#### 1.4 Array.from()
반복 가능한(iterable) 요소들을 배열로 변환하여 반환한다. 

```javascript
const team4 = Array.from(players);
```


### 2. Object 복사하기(call-by-value)
#### 2.1 Object.assign()
첫 번째 인자로 빈 객체를, 두 번째 인자로 복사하려는 원본 객체를, 세 번째 인자로 추가하려거나 새로운 값으로 변경되길 원하는 속성과 값을 전달한다. 

```javascript
const person = {
    name: 'Wes Bos',
    age: 80
};
const cap = Object.assign({}, person, { number: 99, age: 12 });
```

#### 2.2 ES6 Spread 문법

```javascript
const cap2 = {...person};
```

#### 2.3 cloneDeep
위의 방법들은 전부 1레벨까지만 적용된다.    
만약 배열과 객체의 모든 레벨에서 복사(call-by-value)를 하고 싶다면 `clone deep`을 해야 한다. 


> 꼼수!
`JSON.stringify()`는 객체를 문자열로 반환하는데 그 문자열을 바로 `JSON.parse()`를 통해 객체로 변환하면, 전체 값을 복사(call-by-value)하는 것과 같은 효과가 나타난다. 

```javascript
const dev2 = JSON.parse(JSON.stringify(wes));
```