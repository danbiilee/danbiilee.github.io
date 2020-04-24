---
title: "String 래퍼 객체"
category: Javascript
---

## 1. String.prototype.split(separator: string | RegExp[, limit: number]): string[]
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



## 2. String.prototype.substring(start: number[, end: number]): string
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



## 3. String.prototype.slice(start: number[, end: number]): string
- String.prototype.substring()과 동일하나, 음수의 인수를 전달할 수 있는 차이가 있음

``` javascript
const str = 'Hello World';

//뒤에서부터 5자리를 잘라내어 반환
console.log(str.slice(-5)); // World
```



## 4. String.prototype.toLowerCase(): string
- 대상 문자열의 모든 문자를 소문자로 변경 



## 5. String.prototype.toUpperCase(): string
- 대상 문자열의 모든 문자를 대문자로 변경 



## 6. String.prototype.trim(): string
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



## 7. String.prototype.repeat(count: number): string
- 인수로 전달한 수만큼 반복해 연결한 새로운 문자열을 반환
- 인수가 0이면 빈 문자열 반환
- 인수가 음수이면 RangeError를 발생 

``` javascript
console.log('abc'.repeat(0)); // ''
console.log('abc'.repeat(2.5)); // 'abcabc' (2.5 -> 2)
console.log('abc'.repeat(-1));  // RangeError: Invalid count value
```



## 8. String.prototype.includes(searchString: string[, position: number]): boolean
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