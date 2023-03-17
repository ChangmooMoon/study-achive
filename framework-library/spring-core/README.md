# Spring core

{% embed url="https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#spring-core" %}

<figure><img src="../../.gitbook/assets/spring-overview.png" alt=""><figcaption></figcaption></figure>

1. Spring core(core container)

* BeanFactory가 Ioc 패턴을 이용해서 애플리케이션의 설정, 의존성을 애플리케이션 코드에서 분리시킨다.&#x20;
* User interface, Validation, JNDI, EJB, JavaMail지원

2. Spring context

* BeanFactory를 상속받은 ApplicationContext에서 추가적으로 i18n, 라이프사이클, 추가적인 Validation을 지원해서 기능 확장
* Email, JDNI access, EJB 연동, remoting, scheduling 등의 엔터프라이즈 서비스 추가제공, 다른 템플릿 프레임워크와의 통합기능 지원



3. Spring AOP module

* configuration 관리 기능을 통해서 AOP 기능을 지원함. Spring에서 관리하는 모든 객체는 AOP가 가능함
* 트랜잭션 관리 지원(선언적 트랜잭션 작성이 가능해짐)

4. Spring DAO(Data access object)

* Spring JDBC DAO 추상 레이어에서 다른 DB 벤더들의 Exception handling, 에러 메세지를 관리하는 예외계층을 제공함
* JDBC를 이용한 DB access를 지원함. 트랜잭션 관리기능 지원

5. Spring ORM

* 여러 ORM 프레임워크와의 연동을 지원함

6. Spring Web module

* 웹 기반 애플리케이션에 context를 제공함

{% embed url="https://www.baeldung.com/spring-web-contexts" %}

7. Spring MVC framework

* 완전한 MVC 구현을 지원함
* 전략 인터페이스를 통해 설정 가져오는 방식으로 다양한 뷰 기술을 지원함
