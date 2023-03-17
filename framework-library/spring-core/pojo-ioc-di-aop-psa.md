---
description: POJO를 둘러싼 IoC/DI, AOP, PSA 이미지를 기억하자
---

# 스프링 트라이앵글 - POJO, IOC/DI, AOP, PSA

1. **IoC/DI - 제어의 역전, 의존성 주입**

* 객체 내에서 사용할 의존성을 객체 자신이 만들어내지 않고, 내가 사용할 의존성을 누군가가 주입해준다는 개념(IoC, DI)

{% embed url="https://martinfowler.com/articles/injection.html" %}

* 스프링 없이 의존성 주입 - 생성자, 필드를 통한 의존성 주입
*   스프링을 통한 의존성 주입 - XML 설정 파일(property 태그), @Autowired, @Resource

    * 스프링에서는 IoC 컨테이너에 등록된 객체들을 스프링 빈으로 관리한다

    > 참고 자료
    >
    > [https://github.com/spring-attic/understanding/tree/master/application-context](https://github.com/spring-attic/understanding/tree/master/application-context)
    >
    > [https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/ApplicationContext.html](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/ApplicationContext.html)
    >
    > [https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/BeanFactory.html](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/BeanFactory.html)

2. **AOP - Aspect, 관점, 핵심 관심사, 횡단 관심사**

* 스프링 DI는 의존성에 대한 주입, **스프링 AOP는 로직 주입**
* **핵심 관심사**(입금, 출금, 이체 모듈)에서 공통적으로 사용되는 부분(로깅, 보안, 트랜잭션)을 **횡단 관심사**라고 한다(코드 = 핵심 관심사 + 횡단 관심사)
  * 핵심관심사(around)에서 횡단 관심사 기능을 주입할 수 있는 지점 → Before, After, AfterReturning, AfterThrowing
  * 관련 용어들
    * JointPoint - 연결 가능한 지점
    * Pointcut - Aspect 적용 위치 지정자(JointPoint의 부분 집합)
    * Advice - pointcut에 적용할 로직(메서드) + 언제 라는 개념
    * Aspect - Advisor의 집합체(Advice + PointCut)
    * Advisor - 1개의 Advice + 1개의 Pointcut

{% embed url="https://refactoring.guru/design-patterns/proxy" %}

3. **PSA - 일관성 있는 서비스 추상화**

* 어댑터 패턴을 적용해서 같은 일을 하는 다수의 기술을 공통의 인터페이스로 제어하는 것을 서비스 추상화라고 한다.
* ex) JDBC라는 표준 스펙이 있어서 어떤 DB제품을 써도 같은 방식으로 자바 코드를 작성할 수 있다(어댑터 패턴)

{% embed url="https://refactoring.guru/design-patterns/adapter" %}

{% embed url="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/PlatformTransactionManager.html" %}

{% embed url="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/cache/CacheManager.html" %}
