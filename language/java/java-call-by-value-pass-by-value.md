# Java의 Call by value(pass by value)

C++에서의 swap() 유틸리티 함수는 주소값을 교환하는 call by reference 방식으로서 동작한다. tmp 변수를 중간 매개로 주소값(값의 위치)을 서로 교환한다.

```cpp
void swap(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}
```

Java에서 primitive type, reference type에 해당하는 값을 저장하는 방식에 차이가 있다.

* JVM 메모리에서 primitive type은 stack 영역에 저장된다
* reference type은 그 객체인 값이 heap 영역에 저장되고, stack 영역에 있는 변수가 객체의 주소값을 가지고 있다.

![Screen Shot 2022-10-09 at 7.13.01 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f7a510d5-42fc-422c-856d-555f7593607a/Screen\_Shot\_2022-10-09\_at\_7.13.01\_PM.png)

만약 swap 메서드에서 **reference 변수를 파라미터로 넘기게 되면 해당 객체를 가리키는 새로운 변수가 stack 영역에 정의가 된다.** 새롭게 만들어진 변수의 주소값을 서로 교환하거나, 값을 변경한다고 해서 기존의 변수값이 변하지 않는다. 그렇기 때문에 **Java는 항상 call by value(pass by value) 방식으로 동작한다**고 할 수 있다.

* 메서드 호출 방식 개념
  * **Call by value 방식의 메서드 호출 방식**에서 메서드 호출자(caller)와 호출당하는 수신자(callee)의 파라미터는 복사되어서 서로 다른 변수이다. 따라서 수신자의 파라미터를 수정해도 호출자의 변수가 바뀌지 않는다.
  * **call by reference 방식**은 참조(주소)를 직접 전달하기 때문에 caller의 변수와 callee의 파라미터가 완전히 동일한 변수이다. 수신자의 파라미터를 수정하면 호출자의 변수도 바뀐다.
* 자바에서는 기본적으로는 Reference type을 이용해서 swap을 구현해야하지만, primitive 변수 값을 교환하는 트릭도 있다. Collections 패키지에서 list 내의 원소값 간의 swap 메서드를 지원한다.
