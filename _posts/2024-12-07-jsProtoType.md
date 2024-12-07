---
title:  "[javascript] 초등학생도 이해할 ProtoType의 개념과 예제"
excerpt: "자바스크립트 프로토타입이란?"

categories:
  - Blog
tags:
  - [Blog, javascript, Github, Git, md]

toc: true
toc_sticky: true
 
date: 2024-12-07
last_modified_at: 2024-12-07
---
## 프로토타입이란? 
검색해보면 프로토타입은 아래와 같이 나온다.<br>
프로토타입은 자바스크립트가 처음부터 가지고 있던 상속 메커니즘으로, 동적인 특성. 어쩌고 저쩌고... <br>
너무 어렵다. 쉽게 이해할 순 없을까?<br><br>
프로토타입은, 한마디로 **유전자** 라고 표현 할 수 있다.<br>
부모의 특성을 자식도 그대로 물려받는 것. 그게 프로토타입의 끝이다.<br>
예제와 함께 알아가보자.


## 1-1. 프로토타입을 사용하지 않은 경우
```javascript
class Person{
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
}

// person 개별 인스턴스에 이름, 나이 부여
let person = new Person("이주성", 30)

// 변수 선언
let {name, age, skinColor} = person;
console.log("이름 : " + name, "나이 : " + age, "피부색 : " + skinColor);
```
## 1-2. 출력결과
```console
"이름 : 이주성"
"나이 : 30"
"피부색 : undefined"
```
Person 클래스로 인스턴스를 생성할 때, name과 age는 부여하여 정상 출력되었으나 피부색은 undefined이 출력되었다.
다음 예제를 보자.

## 2-1. 프로토타입을 사용한 경우
```javascript
class Person{
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
}

// 프로토타입으로 skinColor 부여
Person.prototype.skinColor = "황인";

// person 개별 인스턴스에 이름, 나이 부여
let person = new Person("이주성", 30)

// 변수 선언
let {name, age, skinColor} = person;
console.log("이름 : " + name, "나이 : " + age, "피부색 : " + skinColor);
```
## 2-2. 출력결과
```console
"이름 : 이주성"
"나이 : 30"
"피부색 : 황인"
```

Person 클래스에 prototype(유전자) 으로 skinColor를 부여하였다.<br>
그로 인해 인스턴스에 별도로 skinColor를 부여하지 않더라도 사용할 수 있게 된다.<br>
**자바스크립트의 Array.length 와 같은 변수나 내부함수들도 이와같은이 프로토타입으로 선언되었기 때문에 사용 할 수 있는 것이다.**


### 장점
1. **유연성**: 프로토타입 기반 상속은 객체를 동적으로 수정할 수 있는 유연성을 제공합니다. 새로운 속성이나 메서드를 런타임에 추가할 수 있습니다.
2. **간단한 상속 구조**: 자바스크립트는 클래스 기반 언어와 달리 복잡한 상속 구조를 필요로 하지 않으며, 프로토타입 체인을 통해 간단하게 상속을 구현할 수 있습니다.
3. **동적 객체 생성**: 객체를 생성할 때마다 새로운 클래스를 정의할 필요 없이, 기존 객체를 기반으로 새로운 객체를 쉽게 생성할 수 있습니다.

<br>

### 단점
1. **복잡한 이해**: 프로토타입 기반 상속은 클래스 기반 상속에 비해 직관적이지 않을 수 있습니다. 특히, 자바스크립트에 익숙하지 않은 개발자에게는 이해하기 어려울 수 있습니다.
2. **디버깅 어려움**: 프로토타입 체인에서 문제가 발생할 경우, 어떤 객체에서 문제가 발생했는지 추적하기 어려울 수 있습니다. 이는 디버깅을 복잡하게 만들 수 있습니다.
3. **명시적이지 않은 상속**: 클래스 기반 언어에서는 상속 관계가 명시적이지만, 자바스크립트에서는 프로토타입 체인을 통해 암묵적으로 이루어지기 때문에 코드의 가독성이 떨어질 수 있습니다.
