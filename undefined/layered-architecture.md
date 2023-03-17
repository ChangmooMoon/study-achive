# Layered Architecture

{% embed url="https://msolo021015.medium.com/layered-architecture-deep-dive-c0a5f5a9aa37" %}

{% embed url="https://isaac56.github.io/etc/2021/08/29/difference_DAO_Repository/" %}

* layered architecture - 관심사의 분리에 따라 시스템을 유사한 책임을 지닌 layer로 분리하고, 각각의 레이어가 하위 레이어에만 의존하도록 구성하는 아키텍쳐 패턴
  1. presentation 레이어
     * HTTP 요청 파라미터, Body를 validation, 사용자의 요청을 위임, 응답을 반환함
     * (추가) 함수(연산) 레벨에서이 명령과 조회의 책임을 분리하는 CQS(command query seperation)을 적용해서 사용자의 요청을 명시적으로 명령과 조회로 분리해서 개발할 수 있음
  2. application 레이어
     * 흐름 제어 목적, AOP를 사용한 종적&횡적 관심사의 분리, 도메인 모델 도입, 단일 책임을 지니는 여러개의 서비스로 분해하고 역할을 위임
     * 단일 개체 서비스를 만들었을 때 단점 → 하는 역할이 너무 많아서 복잡도 증가. 연관성이 적은 개체가 서비스 개체에 밀집하게 되면 의존하는 개체가 많아지고, 그러면 변경에 취약한 코드가 됨
  3. domain 레이어
     * CQS 원칙에 따라 명령 책임과 조회 책임을 분리
     * DIP에 따라 도메인 레이어에서는 고수준의 비지니스 로직을 해결해야되고, 저수준의 기술 구현, 외부 인프라에 의존하지 않도록 구성해야됨
       * [https://techblog.woowahan.com/2561/](https://techblog.woowahan.com/2561/)
       * 도메인 레이어는 추상적이여야되고, 다른 외부 의존성을 참조하지 않아야됨
  4. infrastructure 레이어
     * Data access 기술, IoC 컨테이너, 그 외 기술적인 작업을 수행하는 모든 개체를 포함
       * Spring IoC 환경 구성
       * Session, JWT 보안 기능
       * Data Access(Hibernate나 MyBatis, JDBC)
       * 메세징 큐(Rabbit MQ, Kafka)
       * 메일(JavaMail)
