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

  @AfterReturning(pointcut = "execution(* com.example.service.*.*(..))", returning = "result")
  public void logAfterReturning(Object result) {
      System.out.println("메서드 실행 후: 반환값 = " + result);
  }

  // 예외가 발생한 메서드에 대한 포인트컷 정의
  @AfterThrowing(pointcut = "execution(* com.example.service.*.*(..))", throwing = "ex")
  public void logAfterThrowing(Exception ex) {
    System.out.println("예외 발생: " + ex.getMessage());
  }
}
```

위와 같이 같이 사용 할 수도 있지만, PointCut을 어노테이션을 사용하면 가독성이 좋아지고 불필요한 정의를 줄일 수 있다.
```java
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.AfterThrowing;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    // 포인트컷 정의
    @Pointcut("execution(* com.example.service.*.*(..))")
    public void serviceMethods() {
        // 포인트컷 메서드는 비어 있어야 합니다.
    }

    // Join Point: 특정 메서드 실행 전
    @Before("serviceMethods()")
    public void logBefore() {
        System.out.println("메서드 실행 전: 로그 기록");
    }

    // Join Point: 특정 메서드 실행 후
    @After("serviceMethods()")
    public void logAfter() {
        System.out.println("메서드 실행 후: 로그 기록");
    }

    @AfterReturning(pointcut = "serviceMethods()", returning = "result")
    public void logAfterReturning(Object result) {
        System.out.println("메서드 실행 후: 반환값 = " + result);
    }

    // 예외가 발생한 메서드에 대한 포인트컷 정의
    @AfterThrowing(pointcut = "serviceMethods()", throwing = "ex")
    public void logAfterThrowing(Exception ex) {
        System.out.println("예외 발생: " + ex.getMessage());
    }
}
```
