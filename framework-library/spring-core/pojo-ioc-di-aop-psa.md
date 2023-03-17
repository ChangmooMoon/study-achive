# 스프링 트라이앵글 - POJO, IOC/DI, AOP, PSA

POJO를 둘러싼 IoC/DI, AOP, PSA 이미지를 기억하자

* IoC/DI - 제어의 역전, 의존성 주입
  * 프로그래밍에서의 의존성?
  * 스프링 없이 의존성 주입 - 생성자, 필드를 통한 의존성 주입
  * 스프링을 통한 의존성 주입 - XML 설정 파일(property 태그), @Autowired, @Resource
* AOP - Aspect, 관점, 핵심 관심사, 횡단 관심사
  * 스프링 DI는 의존성에 대한 주입, **스프링 AOP는 로직 주입**
  * **핵심 관심사**(입금, 출금, 이체 모듈)에서 공통적으로 사용되는 부분(로깅, 보안, 트랜잭션)을 **횡단 관심사**라고 한다(코드 = 핵심 관심사 + 횡단 관심사)
    * 핵심관심사(around)에서 횡단 관심사 기능을 주입할 수 있는 곳 → Before, After, AfterReturning, AfterThrowing
    * 관련 용어들
      * JointPoint - 연결 가능한 지점
        * Pointcut - Aspect 적용 위치 지정자(JointPoint의 부분 집합)
        * Advice - pointcut에 적용할 로직(메서드) + 언제 라는 개념
        * Aspect - Advisor의 집합체(Advice + PointCut)
        * Advisor - 1개의 Advice + 1개의 Pointcut
* PSA - 일관성 있는 서비스 추상화
  * 어댑터 패턴을 적용해서 같은 일을 하는 다수의 기술을 공통의 인터페이스로 제어하는 것을 서비스 추상화라고 한다.
  * ex) JDBC라는 표준 스펙이 있어서 어떤 DB제품을 써도 같은 방식으로 자바 코드를 작성할 수 있다(어댑터 패턴)
