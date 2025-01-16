---
title:  "[Spring] 스프링DI의 개념과 자주 사용하는 어노테이션 정리"
excerpt: "스프링 DI의 개념과 자주 사용하는 어노테이션을 정리한다."

categories:
  - Blog
tags:
  - [Blog, Spring Framework, Spring DI, Github, Git, md]

toc: true
toc_sticky: true
 
date: 2024-12-24
last_modified_at: 2024-12-24
---
# Spring DI란?
**의존성 주입(Dependency Injection, DI)**은 객체 간의 의존 관계를 외부에서 주입하는 디자인 패턴으로, 스프링 프레임워크에서 핵심적인 역할을 합니다.
스프링 DI는 애플리케이션의 구성 요소 간의 결합도를 낮추고, 코드의 유연성과 테스트 용이성을 높이는 데 기여합니다.

# DI의 장점
1. **유연성** : 의존성을 외부에서 주입받기 때문에 코드의 유연성이 증가합니다.
2. **모듈화** : 각 컴포넌트가 독립적으로 개발 및 배포될 수 있습니다.

## Maven 의존성 추가
Spring AOP를 사용하기 위해서는 Maven에 의존성을 추가해야 한다.
```xml
<dependencies>
    <!-- Spring Core -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>5.3.10</version>
    </dependency>
    <!-- Spring Context -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.10</version>
    </dependency>
</dependencies>
```


## 예제
### 어노테이션 기반 bean 설정

#### 1. MyRepository 인터페이스와 구현 클래스
```java
public interface MyRepository {
    void doSomething();
}

@Component
public class MyRepositoryImpl implements MyRepository {
    @Override
    public void doSomething() {
        System.out.println("Doing something in MyRepository");
    }
}
```

#### 2. MyService 클래스
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MyService {
    private final MyRepository myRepository;

    @Autowired // 의존성 주입을 위한 어노테이션
    public MyService(MyRepository myRepository) {
        this.myRepository = myRepository;
    }

    public void performAction() {
        myRepository.doSomething();
    }
}
```

#### 3. Spring Boot 애플리케이션 클래스
```java
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

    @Bean
    public CommandLineRunner run(MyService myService) {
        return args -> {
            myService.performAction(); // MyService의 performAction 메서드 호출
        };
    }
}
```

### 설명
1. MyRepository: MyRepository 인터페이스와 그 구현체인 MyRepositoryImpl을 정의합니다. @Component 어노테이션을 사용하여 Spring이 이 클래스를 Bean으로 등록하도록 합니다.
2. MyService: MyService 클래스는 MyRepository에 의존하고 있으며, 생성자에 @Autowired 어노테이션을 사용하여 Spring이 의존성을 주입하도록 합니다.
3. MyApplication: Spring Boot 애플리케이션의 진입점입니다. CommandLineRunner를 사용하여 애플리케이션이 시작될 때 MyService의 performAction 메서드를 호출합니다.

### 실행결과
애플리케이션 실행 시 MyRepository의 doSomething 메서드가 호출되어 "Doing something in MyRepository"라는 메시지가 출력됩니다.
이 예제는 Spring Framework에서 Constructor Injection을 사용하여 의존성을 관리하는 방법을 보여줍니다.
