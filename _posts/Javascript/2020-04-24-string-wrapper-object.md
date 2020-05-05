---
title: "String 래퍼 객체"
category: Javascript
---


프로퍼티나 메소드를 호출할 때 **원시타입과 연관된 래퍼 객체로 일시적으로 변환되어 프로토타입 객체를 공유**하게 되므로, 변수 또는 객체 프로퍼티 값이 문자열이라면 String 객체의 별도 생성없이 String 객체의 프로퍼티와 메소드를 사용할 수 있다. 

## 1. 생성자
- 생성자 함수를 통해 String 객체를 생성할 때 전달된 인자는 모두 문자열로 변환된다.  
- `new` 연산자를 사용하지 않으면 Sring 객체가 아닌 문자열 리터럴을 반환한다. 이 때 형변환이 발생할 수 있다. 

```javascript
// new 연산자 사용
const strObj = new String(undefined);
console.log(strObj); // String {0: 'u', 1: 'n', 2: 'd', 3: 'e' ... } 

// new 연산자 사용하지 않음
var x = String('Lee');
console.log(x); // 'Lee'
```



## 2. 프로퍼티
- length: 문자열의 문자 갯수를 반환한다. String객체는 length 프로퍼티를 소유하고 있으므로 **유사 배열 객체**이다.




## 3. 메소드
문자열은 변경 불가능한 원시값이므로 모든 메소드는 언제나 새로운 문자열을 반환한다.

### 3.1 String.prototype.charAt(pos: number): string
- 인수로 전달한 index에 해당하는 위치의 문자를 반환한다. 
- 전달한 index가 문자열의 범위를 벗어난 경우 빈 문자열을 반환한다.


### 3.2 String.prototype.concat(...strings: string[]): string
- 인수로 전달한 1개 이상의 문자열과 연결해 새로운 문자열을 반환한다. 
- `concat` 메소드보다는 `+`, `+=` 연산자를 사용하는 게 성능상 유리하다.


### 3.3 String.prototype.indexOf(searchString: string[, fromIndex]): number
- 인수로 전달한 문자 또는 문자열을 검색해 처음 발견된 곳의 index를 반환한다. 
- 발견하지 못한 경우 -1을 반환한다. 
- cf) String.prototype.includes(searchString: string): boolean //ES6


### 3.4 String.prototype.lastIndexOf(searchString: string[, fromIndex]): number
- 인수로 전달한 문자 또는 문자열을 검색해 처음 발견된 곳의 index를 반환한다. 발견하지 못한 경우 -1을 반환한다.
- 2번째 인수를 생략할 경우 문자열 길이 -1 부터 역방향으로 검색을 시작한다. 
- 2번째 인수가 전달되면 fromIndex부터 검색을 시작한다.


### 3.5 String.prototype.replace(searchValue: string | RegExp, replaceValue: string | replacer: (match: any[]) ⇒ string): string): string
- 첫번째 인수로 전달한 문자열 또는 정규표현식을 검색해 두번째 인수로 전달한 문자열로 대체한다.
- 첫번째 인수로 전달한 문자열/정규표현식을 검색해 두번째 인수로 전달한 문자열로 대체한다.

```javascript
const str = 'Hello world';

// $& = 검색된 문자열
console.log(str.replace('world', '<strong>$&</strong>')); // Hello <strong>world</strong>


const camelCase = 'helloWorld';

// 1문자와 대문자의 조합을 문자열 전체에서 검색한다. 
// 정규표현식을 괄호로 묶어주면 그 순서대로 $n에 대입해 사용할 수 있다. 
// $1 = (.) = 1문자
// $2 = ([A-Z]) = 대문자
console.log(camelCase.replace(/(.)([A-Z])/g, '$1_$2').toLowerCase()); // hello_world
```



### 3.6. String.prototype.split(separator: string | RegExp[, limit: number]): string[]
- 첫번째 인수로 전달한 문자열/정규표현식으로 구분하여 분리한 후 배열로 반환
- 인수가 없는 경우 대상 문자열 전체를 단일 요소로 하는 배열을 반환 
- 두번째 인수: 구분 대상수의 한계를 나타냄. 생략 가능
  
``` javascript
const str = 'Hello World';

//각 문자를 모두 분리
console.log(str.split('')); // ['H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd' ]

//'o'로 구분하여 배열로 반환. 단 배열의 수는 1개까지만 허용
console.log(str.split('o', 1)); // ['Hell']
```    



### 3.7 String.prototype.substring(start: number[, end: number]): string
- 첫번째 인수인 start인덱스에 해당하는 문자부터 두번째 인수인 end인덱스에 해당하는 문자의 **이전 문자까지**를 반환
- 두번째 인수가 생략된 경우: 문자열 끝까지 반환
- 첫번째 인수 > 두번째 인수: 두 인수는 교환됨
- 인수 < 0 또는 NaN인 경우: 0으로 취급
- 인수 > 문자열 길이인 경우: 문자열 길이로 취급
  
``` javascript
const str = 'Hello World'; // str.length == 11 

//두번째 인수가 생략된 경우: start인덱스부터 문자열 끝까지 반환
console.log(str.substring(4)); // o World

//첫번째 인수 > 두번째 인수: 두 인수는 교환됨
console.log(str.substring(4, 1)); // ell 

//인수 < 0 또는 NaN인 경우: 0으로 취급 -> 문자열 전체가 반환됨 
console.log(str.substring(-2)); // Hello World 

//인수 > 문자열 길이인 경우: 문자열 길이로 취급
console.log(str.substring(1, 12)); // ello World
```



### 3.8 String.prototype.slice(start: number[, end: number]): string
- String.prototype.substring()과 동일하나, 음수의 인수를 전달할 수 있는 차이가 있음

``` javascript
const str = 'Hello World';

//뒤에서부터 5자리를 잘라내어 반환
console.log(str.slice(-5)); // World
```



### 3.9 String.prototype.toLowerCase(): string
- 대상 문자열의 모든 문자를 소문자로 변경 



### 3.10 String.prototype.toUpperCase(): string
- 대상 문자열의 모든 문자를 대문자로 변경 



### 3.11 String.prototype.trim(): string
- 대상 문자열 양쪽 끝의 공백을 제거하여 반환 
- String.prototype.{trimStart, trimEnd}: 문자열 시작 혹은 끝의 공백을 제거 
  
``` javascript
const str = '   foo  ';

// String.prototype.replace로 대체 가능 
// 정규표현식 패턴 \s == 공백 문자 
console.log(str.replace(/\s/g, '')); // 'foo'
console.log(str.replace(/^\s+/g, '')); // 'foo  '
console.log(str.replace(/\s+$/g, '')); // '   foo'
```



### 3.12 String.prototype.repeat(count: number): string
- 인수로 전달한 수만큼 반복해 연결한 새로운 문자열을 반환
- 인수가 0이면 빈 문자열 반환
- 인수가 음수이면 RangeError를 발생 

``` javascript
console.log('abc'.repeat(0)); // ''
console.log('abc'.repeat(2.5)); // 'abcabc' (2.5 -> 2)
console.log('abc'.repeat(-1));  // RangeError: Invalid count value
```



### 3.13 String.prototype.includes(searchString: string[, position: number]): boolean
- 인수로 전달한 문자열이 포함되어있는지를 검사하고 boolean값을 반환
- 두번째 인수: 검색할 위치를 나타내는 정수. 생략 가능

``` javascript
const str = 'Hello World';

console.log(str.includes('hello')); // true
console.log(str.includes('')); // true
console.log(str.includes()); // false

// String​.prototype​.indexOf 메소드로 대체 가능
console.log(str.indexOf('hello')); // 0
```