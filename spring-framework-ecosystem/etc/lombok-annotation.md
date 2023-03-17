# Lombok annotation, 권장 방식

#### NoArgsConstructor : 매개 변수가 없는 기본 생성자를 생성

* force : final 필드가 존재할 때 이를 null 또는 0으로 초기화해 기본 생성자를 만들 수 있게 한다.
* access : 생성되는 메소드의 접근제어자 설정 (AccessLevel)
* onConstructor\_ = {@어노테이션,...} : 생성된 생성자에 어노테이션 추가
* staticName : 해당 생성자를 사용하는 static 생성자를 추가

***

#### @RequiredArgsConstructor : final 필드만 포함된 생성자를 생성

* access : 생성되는 메소드의 접근제어자 설정 (AccessLevel)
* onConstructor\_ = {@어노테이션,...} : 생성된 생성자에 어노테이션 추가
*   staticName : 해당 생성자를 사용하는 static 생성자를 추가

    * of로 정의하는 패턴 많이 볼 수 있음

    [https://johngrib.github.io/wiki/pattern/static-factory-method/#lombok-requiredargsconstructorstaticname%EC%9D%98-%EC%82%AC%EC%9A%A9](https://johngrib.github.io/wiki/pattern/static-factory-method/#lombok-requiredargsconstructorstaticname%EC%9D%98-%EC%82%AC%EC%9A%A9)

***

#### @AllArgsConstructor : 모든 필드를 포함한 생성자를 생성

* access : 생성되는 메소드의 접근제어자 설정 (AccessLevel)
* onConstructor\_ = {@어노테이션,...} : 생성된 생성자에 어노테이션 추가
* staticName : 해당 생성자를 사용하는 static 생성자를 추가

***

### 메소드 관련

***

#### @Getter : Getter를 자동으로 생성

* lazy : Getter를 캐시 하며, Getter가 CPU가 많이 필요하거나 메모리가 많이 필요한 표현식의 경우 유용 (private final 변수에만 사용 가능, 롬복에서 잠금 처리하여 Thread-safe일 필요 없다.)
* onMethod\_ = {@어노테이션,...} : 생성되는 메소드에 어노테이션 추가
* value : 생성되는 메소드의 접근제어자 설정 (AccessLevel)

***

#### @Setter : Setter를 자동으로 생성

* onParam\_ = {@어노테이션,...} : Setter의 매개 변수에 어노테이션 추가
* onMethod\_ = {@어노테이션,...} : 생성되는 메소드에 어노테이션 추가
* value : 생성되는 메소드의 접근제어자 설정 (AccessLevel)

***

#### @ToString : toString 메소드를 자동으로 생성

* includeFieldNames : 이름-값 쌍으로 표현할지 값만 표현할지 여부
* of : 포함할 필드 설정
* exclude : 제외할 필드 설정
* callSuper : 슈퍼 클래스의 toString 메소드 출력을 포함시킬지 여부
* doNotUseGetters : toString 메소드 구현에 Getter 메소드를 사용하지 않고 this를 사용할지 여부
* onlyExplicitlyIncluded : 필드에 설정된 @ToString.Include 또는 @ToString.Exclude를 적용시킨다

***

#### @EqualsAndHashCode : equals, hashCode 메소드를 자동으로 생성

* cacheStrategy : hashCode의 호출 결과를 캐시하여 이후 호출에 사용할지 여부
* of : 포함할 필드 설정
* exclude : 제외할 필드 설정
* callSuper : 슈퍼 클래스의 toString 메소드 출력을 포함시킬지 여부
* doNotUseGetters : toString 메소드 구현에 Getter 메소드를 사용하지 않고 this를 사용할지 여부
* onlyExplicitlyIncluded : 필드에 설정된 @EqualsAndHashCode.Include 또는 @EqualsAndHashCode.Exclude를 적용시킨다.

***

#### @With : with 메소드를 자동으로 생성

with 메소드는 해당 필드만 인자로 전달한 값으로 변경하여, 모든 필드를 사용한 생성자를 통해 새로운 객체로 반환한다. (해당 객체의 필드와 동일한 값을 설정하면 해당 객체를 반환한다.)

* onParam\_ = {@어노테이션,...} : with 메소드의 매개 변수에 어노테이션 추가
* onMethod\_ = {@어노테이션,...} : with 메소드에 어노테이션 추가
* value : 생성되는 메소드의 접근제어자 설정 (AccessLevel)

***

### 통합 기능

***

#### @Data : 여러 어노테이션 통합

@ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor 기능을 함께 제공

* staticConstructor : final 변수로 이루어진 static 생성자를 만든다. (@RequiredArgsConstructor를 private로 생성)

***

#### @Value : @Data의 변형된 기능

모든 필드를 private final로 설정, 클래스를 final로 설정, Setter를 생성하지 않는다.

* staticConstructor : final 변수로 이루어진 static 생성자를 만든다. (@RequiredArgsConstructor를 private로 생성)

***

### 빌더 패턴

***

#### @Builder : 메소드 체이닝을 이용하는 static 메소드 builder()를 생성한다.

생성자 대신 편리하게 사용

* access : builder()의 접근제어자 설정 (AccessLevel)
* builderClassName : builder의 클래스 이름을 명시적으로 설정
* builderMethodName : builder()의 메소드 이름을 명시적으로 변경
* buildMethodName : build()의 메소드 이름을 명시적으로 변경
* toBuilder : 인스턴스의 현재 값을 가지고 시작하는 builder를 생성
* setterPrefix : Setter 메소드의 이름 앞에 해당 문자열을 붙인다.

***

#### @Builder.Default : 명시적으로 기본값 설정

필드에 값을 설정하지 않은 경우 0/null/false로 기본값이 설정된다.이때 기본값을 지정하기 위해 사용

***

#### @Singular : 해당 필드를 컬렉션으로 처리하여 다수의 값을 할당할 수 있다.

값을 비우는 clear 메소드가 함께 생성된다.

* ("필드명") : 컬렉션의 값을 할당할 때 사용할 필드명을 따로 지정한다.(기존 필드명은 컬렉션 자체를 할당할 때 사용된다.)

***

### 그 외

***

#### @NonNull : null-check 로직을 자동으로 생성하여 null 값이 넘어온 경우 NulPointerException 발생

기본 생성자 대신 해당 필드를 포함한 생성자가 추가된다.

***

#### @Cleanup : 해당 영역을 벗어날 때 지정된 리소스의 close()를 호출

try-finally 구문이 적용된다.

* ("메소드명") : close()가 아닌 dispose()와 같은 리소스를 닫는 메소드를 호출하고자 할 때 속성으로 해당 메소드명 기입(매개 변수가 있는 메소드는 호출할 수 없다.)

***

#### @Synchronized : java의 synchronized의 더 안전하게 변형된 기능

static, instance 단위로 락을 거는 synchronized와 다르게 필드 단위로 락을 건다. (메소드에만 사용 가능)

* ("필드명") : 해당 필드에 락을 건다.

***

#### @SneakyThrows(예외클래스) : try-catch 문법으로 해당 예외를 처리

Checked Exception 처리에 유용

***

#### @Log, @CommonsLog, @Log4j2, @Slf4j 등...

로그 프레임워크를 log라는 이름의 private static final 필드로 생성한다.



{% embed url="https://velog.io/@bwjhj1030/DTO-%EB%A7%8C%EB%93%A4-%EB%95%8C-Lombok-%EA%BF%80%ED%8C%81-%EB%8C%80%EB%B0%A9%EC%B6%9C" %}

{% embed url="https://cheese10yun.github.io/lombok/" %}

{% embed url="https://levelup.gitconnected.com/be-careful-with-lombok-2e2edfc01110" %}

{% embed url="https://medium.com/geekculture/good-and-bad-usage-of-lombok-8c8f70874a93" %}
