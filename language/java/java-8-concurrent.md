---
description: 리액티브 자바는 나중에 정리... 너무 어렵다
---

# java 8 Concurrent

* Concurrent programming - Executor, Callable, Future, CompletableFuture
  * Thread 상속을 통해서 쓰레드 구현하는 것과 Runnable을 구현해서 쓰레드 구현하는 것을 알아야함
  * 쓰레드의 주요 기능들 sleep, interrupt, join. 이것 만으로는 어떤 작업을 멀티스레딩 처리하는 것이 힘듬. 좀 더 고수준의 Concurreny 프로그래밍이 필요함
  * **Executors** - 쓰레드 관리 작업을 애플리케이션에서 분리하고 Executors에 위임.
    * 쓰레드 만들기, 관리, 작업처리 및 실행 API 제공
    * 주로 **ExecutorService**를 쓰게 됨
    * 쓰레드로 태스크 하나를 처리했다면 명시적으로 종료하지 않으면 대기하게 됨. shutdown() : graceful shutdown. 지금까지의 작업은 다 마치고 shutdown, 당장 끝내고 싶다면 shutdownNow()
    * 자바 Main에서 ExecutorService 실행했을 때 의 ES 구조: 쓰레드 풀 앞에 blocking queue가 있음. 쓰레드에서 작업을 처리하는 동안 blocking queue에 쌓아둠
  * **Callable, Future** - runnable은 타입이 void인 단점이 있음. Java 1.5의 Callable을 이용해서 리턴을 할 수 있음. 이 리턴값을 받아오는 것이 Future이다.
    * isDone(), cancel(), invokeAll(), invokeAny()
  * **CompletableFuture**
    * java 1.5의 Future, CompletionStag를 구현해놓음
    * 비동기 처리가 쉬워짐.
    * executor를 구현한 ForkJoinPool은 deque를 사용해서 자기 쓰레드가 할일이 없으면 deque에서 작업을 가져와서 처리함. 한 작업의 sub작업을 다른 쓰레드에 배분함
    * 비동기 작업실행- RunAsync(), supplyAsync()
    * 콜백 제공- thenApply(F), thenAccept(Consumer), thenRun(Runnable)
    * 조합
      * thenCompose() - 서로 연관관계(의존성)이 있을 경우
      * thenCombine() - 별개의 작업 ex) 각각의 주식가격을 로드하고 다 처리됬을 때 다음 작업을 처리하는 경우
      * allOf() - (태스크가 반환값이 있어야 작업처리 확인이 쉬움) 모든 태스크가 다 끝났다면, thenAccept()…로 처리한다.
      * anyOf() - 가장 먼저 끝난 하나의 작업에 콜백 실행
    * 예외처리
      * exeptionally(Func) - 에러 처리
      * handle(BiFunction) - good, error 처리

{% embed url="https://winterbe.com/posts/2015/04/07/java8-concurrency-tutorial-thread-executor-examples/" %}

[https://ellerymoon.tistory.com/118](https://ellerymoon.tistory.com/118)
