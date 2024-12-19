---
title:  "[javascript] 자바스크립트 콜백함수 개념이해 및 promise, async/await 사용법 정리"
excerpt: "자바스크립트 콜백이란?"

categories:
  - Blog
tags:
  - [Blog, javascript, Github, Git, md]

toc: true
toc_sticky: true
 
date: 2024-12-14
last_modified_at: 2024-12-14
---
## 콜백함수란? 
콜백함수는 파라메타로 전달받은 함수를 의미한다.
파라메타로 콜백을 전달받고 내부에서 콜백함수를 호출하는 형태이다.
a함수와 b함수를 실행한다고 가정했을 때 자바스크립트는 a함수가 끝날때까지 b함수가 기다려주지 않는다.
때문에 순차 처리를 위한 콜백함수가 필요하다.

## 1-1. 콜백함수 예제
```javascript
// 콜백 함수를 정의합니다.
function greeting(name) {
    console.log("안녕하세요, " + name + "!");
}

// 다른 함수에서 콜백 함수를 사용합니다.
function processUserInput(callback) {
    const name = prompt("이름을 입력하세요:");
    callback(name); // 콜백 함수를 호출합니다.
}

// processUserInput 함수에 greeting 함수를 콜백으로 전달합니다.
processUserInput(greeting);
```

## 1-2. 출력결과
```console
1. 팝업창 출력 -> 이름을 입력하세요 : {이름입력}
2. 콘솔 출력 -> "안녕하세요, {이름}!"
```

## 2-1. promise를 이용한 콜백
### 순차처리를 하지 않았을 경우
```javascript
function fnStart1() {
  setTimeout(() => {
    console.log("start1 END!");
  }, 3000);

}

function fnStart2() {
        setTimeout(() => {
            console.log("start2 END!");
        }, 2000);

}

function fnStart3() {
    console.log("start3 END!"); // fnStart3는 즉시 실행
}

fnStart1();
fnStart2(); // fnStart1이 끝난 후 fnStart2 실행
fnStart3(); // fnStart2가 끝난 후 fnStart3 실행
```
### 출력결과
```console
console.log("start3 END!");
console.log("start2 END!");
console.log("start1 END!");
```


### 순차처리를 한 경우
```javascript
function fnStart1() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("start1 END!");
            resolve(); // fnStart1이 끝나면 resolve 호출
        }, 3000);
    });
}

function fnStart2() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("start2 END!");
            resolve(); // fnStart2가 끝나면 resolve 호출
        }, 2000);
    });
}

function fnStart3() {
    console.log("start3 END!"); // fnStart3는 즉시 실행
}

// Promise를 사용하여 순차적으로 실행
fnStart1()
    .then(fnStart2) // fnStart1이 끝난 후 fnStart2 실행
    .then(fnStart3); // fnStart2가 끝난 후 fnStart3 실행
```
### 출력결과
```console
console.log("start1 END!");
console.log("start2 END!");
console.log("start3 END!");
```

아래와 같이 async await를 이용하여 콜백을 구현 할 수도 있다.
## 3-1. async await를 이용한 콜백
```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function fnStart1() {
    await delay(3000); // 3초 대기
    console.log("start1 END!");
}

async function fnStart2() {
    await delay(2000); // 2초 대기
    console.log("start2 END!");
}

async function fnStart3() {
    console.log("start3 END!"); // 즉시 실행
}

async function runFunctions() {
    await fnStart1(); // fnStart1 실행
    await fnStart2(); // fnStart2 실행
    await fnStart3(); // fnStart3 실행
}

runFunctions();
```
