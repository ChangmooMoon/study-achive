# Stream

* 스트림의 정의
  * **데이터 처리 연산을 지원하도록 소스에서 추출된 연속된 요소**
    * 스트림은 특정 요소 형식으로 이루어진 연속된 값 집합의 인터페이스를 제공한다(filter, sorted, map 같은 표현 **계산**식) ↔ 컬렉션은 **데이터**의 자료구조를 제공함
    * 스트림은 컬렉션, 배열, I/O 자원 등의 데이터 제공 소스로부터 데이터를 소비한다. 입력 그대로 같은 출력순서를 유지한다
    * 스트림은 fp에서 일반적으로 지원하는 연산, 데이터베이스와 비슷하게 filter, map, reduce, find, match, sort 등으로 데이터르르 조작할 수 있고 이를 순차적 또는 병렬로 실행할 수 있다
* 스트림 특징
  * **파이프라이닝** - 스트림 연산끼리 연결해서 파이프라인을 구성할 수 있도록 스트림 자기 자신을 반환한다 - laziness, short-circuiting 최적화가 가능해짐
    * 데이터 소스를 받아서 스트림을 구성하고, filter, map, limit,로 이어지는 일련의 데이터 처리 연산을 적용하고, collect로 파이프라인을 처리해서 결과를 반환한다. collect가 호출되기 전까지는 아무 연산도 일어나지 않는다.(메서드 호출이 저장됨. 지연연산)
    * collect는 스트림을 다른 형식으로 변환한다(toList()로 리스트 변환)
  * **내부 반복** - 내부 반복을 지원함 ↔ 컬렉션은 반복자를 이용해서 명시적으로 반복한다.
* 스트림과 컬렉션의 차이, 배경
  * 공통점 - 자바 컬렉션, 스트림은 연속된 요소 형식의 값을 저장하는 자료구조의 인터페이스를 제공한다
  * 차이점
    1. **데이터를 언제 계산하는 지의 여부**
       * 컬렉션은 현재 자료구조가 포함하는 모든 값을 메모리에 저장하는 자료구조이다(적극적 생성 - 모든 값을 계산할 때 까지 기다린다. DVD에 저장된 영화)
       * 스트림은 요청할 때만 요소를 계산하는 고정된 자료구조이다(게으른 생성 - 필요할 때만 값을 계산한다. 스트리밍 서비스에서 순차적으로 들어오는 패킷 연산)
         * **스트림의 요소는 요청할 때 게으르게 계산된다**
    2. **한번 소비된 스트림은 다시 탐색할 수 없음**
       *   **스트림은 한번만 탐색할 수 있다. 한번 탐색한 스트림을 다시 탐색하려면 새로운 스트림을 만들어야한다(단 한번만 소비할 수 있다)**

           ```java
           Stream<String> s = menu.stream();
           s.forEach(System.out::println);
           s.forEach(System.out::println); // java.lang.IllegalStateException이 발생함. 스트림이 이미 소비되었거나 닫힘
           ```
       *   스트림 재사용 불가

           * [https://stackoverflow.com/questions/36255007/is-there-any-way-to-reuse-a-stream](https://stackoverflow.com/questions/36255007/is-there-any-way-to-reuse-a-stream)
           * [https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html)

           A stream should be operated on (invoking an intermediate or terminal stream operation) only once.

           A stream implementation may throw IllegalStateException if it detects that the stream is being reused.

           * 재할당을 하거나 새로운 스트림 객체를 반환하는 Supplier를 구현할 수 있다.
    3. 외부 반복, 내부 반복
       * 컬렉션 인터페이스를 순회하려면 사용자가 직접 요소를 반복해야 된다. (iterator나 foreach문으로 명시적인 반복문으로 순회한다. 내부적으로 숨겨진 iterator를 사용해서 외부 반복)
       *   **스트림 라이브러리는 filter, map, sorted 등의 연산으로 반복을 추상화해서 알아서 처리하고, 결과 스트림값을 저장해주는 내부 반복을 사용한다(iterator가 필요없음)**

           ```java
           List<String> names = new ArrayList<>();
           for(Dish dish: menu) {
           	names.add(dish.getName());
           }
           List<String> names = menu.stream()
           	.map(Dish::getName)
           	.collect(toList());
           ```
       * 스트림의 내부반복이 컬렉션의 외부반복보다 더 좋은 2가지 이유
         1. filter나 map 등의 중간연산이 제공하는 내부반복을 이용하면 작업을 투명하게 병렬로 처리할 수 있고, 더 최적화된 다양한 순서로 처리할 수 있다.
         2. 스트림 라이브러리의 내부 반복은 데이터 표현과 병렬성 구현을 자동으로 선택하지만 외부반복의 경우 병렬성을 synchronized 등으로 스스로 관리해야한다(스트림 API 내부적으로 코드를 병렬로 실행할지 말지를 선택할 수 있다)
