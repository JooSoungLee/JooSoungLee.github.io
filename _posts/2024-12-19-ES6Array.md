---
title:  "[ES6] 자주 사용하는 배열 메서드 정리
excerpt: "ES6 배열 메서드 정리"

categories:
  - Blog
tags:
  - [Blog, ES6, Github, Git, md]

toc: true
toc_sticky: true
 
date: 2024-12-19
last_modified_at: 2024-12-19
---
# 1. ES6 배열 메서드
ES6에서는 유용한 Array 메서드가 제공된다.
불필요한 for문 if문 없이 간단하게 기능 사용이 가능하고
코드의 가독성이 좋아지며
세련된 ES6 Array 메서드를 알아보자

## 1-1. forEach 
```javascript
// 배열의 각 요소에 대해 함수를 실행
fruits.forEach(fruit => console.log(fruit));
```
## 1-2 map
```javascript
// 배열의 각 요소를 변환하여 새로운 배열을 생성합니다.
const lengths = fruits.map(fruit => fruit.length); // [5, 6, 6]
```

## 1-3 filter
```javascript
// 조건에 맞는 요소만 추출하여 새로운 배열을 생성합니다.
const longFruits = fruits.filter(fruit => fruit.length > 5); // ['banana', 'cherry']
```

## 1-4 find
```javascript
// 조건에 맞는 첫 번째 요소를 반환합니다.
const found = fruits.find(fruit => fruit.startsWith('b')); // 'banana'
```

## 1-6 includes
```javascript
// 배열에 특정 요소가 포함되어 있는지 확인합니다.
const hasBanana = fruits.includes('banana'); // true
```

## 1-7 indexOf
```javascript
// 배열에 특정 요소가 포함되어 있는지 확인합니다.
const index = fruits.indexOf('cherry'); // 2
```

## 1-7 sort
```javascript
// 배열을 정렬합니다.
const sortedFruits = fruits.sort(); // ['apple', 'banana', 'cherry']
```
