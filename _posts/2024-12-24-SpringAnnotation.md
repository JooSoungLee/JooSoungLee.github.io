---
title:  "[Spring Framework] 스프링AOP 자주 사용하는 어노테이션 정리"
excerpt: "스프링 AOP에서 자주 사용하는 어노테이션을 정리한다."

categories:
  - Blog
tags:
  - [Blog, Spring Framework, Spring AOP Github, Git, md]

toc: true
toc_sticky: true
 
date: 2024-12-24
last_modified_at: 2024-12-24
---
# Spring AOP란?
AOP(Aspect-Oriented Programming) 은 관심사 분리를 목표로 하는 프로그래밍 기법이다.<br>
특정 기능(예:로깅, 보안, 트랜잭션 등)을 비즈니스 로직과 분리하여 코드의 중복을 줄이고,<br>
가독성과 유지보수성을 높이는데 도움을 준다.<br>
AOP 기법 중 자주 사용하는 어노테이션 기법을 정리해 보자.

## Maven 의존성 추가
Spring AOP를 사용하기 위해서는 Maven에 의존성을 추가해야 한다.
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

## 주요 개념
- **Aspect**     : 공통 관심사를 모듈화한 것. 보통 클래스 단위로 구성된다. 예를 들어, 로깅이나 트랜잭션 관리가 이에 해당한다.
- **Join Point** : Aspect가 적용될 수 있는 지점으로, 메서드 호출, 객체 생성 등 다양한 지점이 될 수 있음.
- **Point Cut**  : Join Point의 집합으로, 어떤 Join Point에 Aspect를 적용할지를 정의한다. 주로 표현식으로 작성됨. 

## 어노테이션 별 개념 정리
- **@Aspect**          : 공통 관심사를 모듈화. 업무단위별로 하나의 Aspect를 구성
- **@Before**          : Join Point 실행 전에 실행됨.
- **@After**           : Join Point 실행 후에 실행됨.
- **@After Returning** : Join Point가 정상적으로 실행된 후에 실행됨.
- **@After Throwing**  : Join Point에서 예외가 발생했을 때 실행됨.


## 예제
### 1-1. Aspect 클래스 정의 : 공통 관심사를 정의하는 Aspect 클래스를 만든다.
```java
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAcpect {
  // Join Point : 특정 메서드 실행 전
  // 첫 번째 *: 이 부분은 반환 타입을 나타냅니다. *는 모든 반환 타입을 의미합니다. 즉, 어떤 반환 타입의 메서드에도 이 Advice가 적용될 수 있습니다.
  // com.example.service: 이 부분은 패키지 이름을 나타냅니다. com.example.service 패키지 내의 모든 클래스가 대상이 됩니다.
  // 두 번째 *: 이 부분은 클래스 이름을 나타냅니다. *는 모든 클래스 이름을 의미합니다. 즉, com.example.service 패키지 내의 모든 클래스의 메서드가 대상이 됩니다.
  // 세 번째 *: 이 부분은 메서드 이름을 나타냅니다. *는 모든 메서드 이름을 의미합니다. 즉, 해당 클래스 내의 모든 메서드가 대상이 됩니다.
  // (..): 이 부분은 메서드의 매개변수를 나타냅니다. ..는 0개 이상의 매개변수를 의미합니다. 즉, 매개변수가 없거나 여러 개일 수 있는 모든 메서드가 대상이 됩니다.
  @Before("excution(* com.example.service.*.*(..))")
  public void logBefore(){
    System.out.println("메서드 실행 전: 로그 기록");
  }

  // Join Point: 특정 메서드 실행 후
  @After("execution(* com.example.service.*.*(..))")
  public void logAfter() {
    System.out.println("메서드 실행 후: 로그 기록");
  }
}
```

### 1-2. Aspect 클래스 정의 : 공통 관심사를 정의하는 Aspect 클래스를 만든다.



## 1. 변수 선언의 방식 차이 (var, let, const)
- **var**: 재정의와 재선언 모두 가능.
- **let**: 재정의 가능하지만 재선언은 불가능.
- **const**: 재선언과 재정의 모두 불가능.

```javascript
// var 예제 
if(1=1){
    var x=1 // 정상동작
    var x=2 // 정상동작
    x=3     // 정상동작
}

// let 예제 
if(1=1){
    let x=1 // 정상동작
    x=1     // 정상동작
    let x=1 // 오류 발생 Uncaught SyntaxError: Invalid left-hand side in assignment
}

// const 예제
if(1=1){
    const x=1 // 정상동작
    x=1       // 오류 발생 Uncaught SyntaxError: Invalid left-hand side in assignment
    let x=1   // 오류 발생 Uncaught SyntaxError: Invalid left-hand side in assignment
}
```

### 1-1 장점
1. **코드 수정 시 안전성**: 변수를 재선언할 수 없기 때문에, 코드 수정 시 기존 변수를 실수로 덮어쓰는 위험이 줄어듭니다.
2. **명확한 변수 사용**: 변수를 한 번 선언하고 재정의만 하도록 제한함으로써, 코드에서 변수가 어떤 역할을 하는지 명확하게 알 수 있습니다



## 2. 클래스 (Class)
ES6에서는 객체 지향 프로그래밍을 지원하기 위해 클래스를 도입했습니다. 클래스는 상속을 통해 다른 클래스로부터 속성과 메서드를 물려받을 수도 있습니다.

### 2-1 기본 클래스 정의
`class` 키워드를 사용하여 정의하며. 생성자는 `constructor` 메서드로 정의. 객체가 생성될 때 호출됩니다.
```javascript
class Animal {
    constructor(name) {
        this.name = name; // 인스턴스 변수
    }

    speak() {
        console.log(`${this.name}가 소리칩니다.`);
    }
}

const dog = new Animal('강아지');
dog.speak(); // 출력: 강아지가 소리칩니다.
```

### 2-2 상속 클래스 정의
```javascript
class Dog extends Animal {
    constructor(name, breed) {
        super(name); // 부모 클래스의 생성자 호출
        this.breed = breed; // 추가 속성
    }

    speak() {
        console.log(`${this.name}(${this.breed})가 멍멍합니다.`);
    }
}

const myDog = new Dog('바둑이', '진돗개');
myDog.speak(); // 출력: 바둑이(진돗개)가 멍멍합니다.
```

### 2-3 장점
1. **코드 재사용성**: 클래스를 사용하면 코드의 재사용성이 높아집니다. 상속을 통해 기존 클래스를 확장하고, 공통 기능을 부모 클래스에 정의하여 자식 클래스에서 재사용할 수 있습니다.
2. **캡슐화**: 클래스는 데이터와 메서드를 하나의 단위로 묶어 관리할 수 있게 해줍니다. 이를 통해 데이터 보호와 코드의 가독성을 높일 수 있습니다.
3. **유지보수 용이성**: 클래스 기반의 구조는 코드의 유지보수를 용이하게 합니다. 각 클래스는 특정 기능을 담당하므로, 수정이나 추가가 필요할 때 해당 클래스만 수정하면 됩니다.



## 3. 구조 분해/할당방식 용이
### 3-1 배열이나 객체의 값을 쉽게 추출할 수 있다.
```javascript
const arr = [1, 2, 3];
const [a, b] = arr;
console.log(a, b); // 출력: 1 2

const obj = { x: 1, y: 2 };
const { x, y } = obj;
console.log(x, y); // 출력: 1 2
```

### 3-2 배열이나 객체를 쉽게 복사하거나 결합할 수 있다.
```javascript
function sum(...numbers) {
    return numbers.reduce((acc, curr) => acc + curr, 0);
}

//파라메타 1,2,3 입력시 배열로 파라메타를 받는다.
const summery = sum(1, 2, 3);
console.log(summery); // 출력: 6

const arr1 = [1, 2];
const arr2 = [3, 4];
// ...문법으로 배열을 합칠 수 있다.
const combined = [...arr1, ...arr2];
console.log(combined); // 출력: [1, 2, 3, 4]
```

### 3-3 장점
1. **코드의 간결화**:코드가 간결해집니다.
2. **가독성**:코드의 가독성이 좋아집니다.

