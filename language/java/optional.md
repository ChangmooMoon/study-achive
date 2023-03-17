# Optional

* **비어있거나 하나 이상 담을 수 있는 컨테이너 인스턴스의 타입**
* 어떤 리스트가 비어있는데 원소를 꺼내서 출력을 하는 경우
  * 예외를 던지는 것은 스택트레이스를 남기기 때문에 비용이 비쌈.
  * null을 던지는 것은 클라이언트가 이를 위해 예외처리를 해야된다
  * Optional 타입으로 래핑해서 클라이언트에게 명시적으로 빈 값일 수도 있다고 알려주고, 빈 값인 경우에는 처리를 강제한다
* 리턴값으로만 쓰기를 권장한다. 매개변수, 맵의 key 타입, 인스턴스의 필드타입으로 쓰지 말자. 매개변수로 쓸 경우 문법적으로 오류가 아니지만, 바디에서 null인지 아닌지를 체크해야되고, 번거로워짐
  * 매개변수로 쓰는 경우 문법적으로는 오류가 아니지만, 바디에서 isPresent로 null 체크를 해야되고, 파라미터 자체도 null 체크를 해야되서 Optional을 쓰는 의미가 없어짐
  * Map의 키는 null이 될 수 있다는 것은 규칙을 깨는 것임
* Primitive 타입용 Optional 이 각각 따로 있다. OptionalInt, OptionalLong…
* collection, Map, Stream, Array, Optional은 Optional로 감싸지 말자
* 이펙티브 자바 item 55. 적절한 경우에 Optional을 리턴하라
* [https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html)
* [https://www.oracle.com/technical-resources/articles/java/java8-optional.html](https://www.oracle.com/technical-resources/articles/java/java8-optional.html)
* 자주 쓰는 API
  * Optional 만들기 - **of(), ofNullable(), empty()**
  * Optional 에 값이 있는지 확인하기 - **isPresent(), isEmpty() - java11**
  * Optional에 있는 값 가져오기 - **get()**
  * 비어있는 Optional에서 값을 꺼내는 경우 - **ifPresent(consumer)**
    * ‘spring’으로 시작하는 수업이 있으면 id를 출력해라
  * Opiontal에 값이 있으면 가져오고 없으면 - **getElseGet(Supplier)**
    * ‘JPA’로 시작하는 수업이 있으면 새로 만들어서 리턴해라
  * Optional에 값이 있으면가져오고, 없으면 에러를 던진다 - **orElseThrow()**
  * Optiontal에 들어있는 값 걸러내기 - **Optional filter(predicate)**
  *   Optiontal에 들어있는 값 변환하기 - **Optional map(Func), Optiontal flatMap(Func)**

      ↔ stream의 flatmap 은 input은 하나인데 output이 여러개가 나오는 경우 flatmap 으로 1대1매칭시켜주는 방식을 사용함
