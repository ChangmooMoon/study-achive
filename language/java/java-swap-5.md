# Java 변수 간 값 Swap 방식 5가지

1. **Swapping primitives -** swap 메서드에서 b, a를 대입한 b를 파라미터로 넘겨주고 받은 리턴값 b를 a에 대입한다

```java
class Main {
	public static int swap(int... args) { return args[0]; }

	public static void main(String[] args) {
		int a = 5;
		int b = 10;
		a = swap(b, b = a); // a = 10, b = 5		
	}
}
```

2. **Swapping array elements -** 교환할 값이 배열의 요소이면 배열인덱스로 접근해서 교환하는 메서드를 짤 수 있다.

```java
class Main {
    public static void swap(int[] arr int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
 
    public static void main(String[] args) {
        int[] arr = { 1, 2, 3, 4, 5 };
        swap(arr, 2, 3);
    }
}
```

3. Swapping Objects, AtomicInteger - 객체로 wrapping해서 내부 값을 교환하는 방식

```java
class Main {
	public static void swap(IntRef a, IntRef b) {
		int tmp = a.val;
		a.val = b.val;
		b.val = tmp;
	}

	public static void main(String[] args) {
		IntRef a = new IntRef(5);
		IntRef b = new IntRef(10);
		swap(a, b); // a.val = 10, b.val = 5
	}
}
```

4. java.util.concurrent.atomic.AtomicInteger로 wrapping할 수도 있다.

```java
import java.util.concurrent.atomic.AtomicInteger;

class Main {
	public static void swap(AtomicInteger a, AtomicInteger b) {
		a.set(b.getAndSet(a.get()));
	}

	public static void main(String[] args) {
		AtomicInteger a = new AtomicInteger(5);
		AtomicInteger b = new AtomicInteger(10);
		swap(a, b);
	}
}
```

5. **Collections.swap(list, i, j);**

* `public static void swap(List<?> list, int i, int j)`

{% embed url="https://www.techiedelight.com/swapping-primitives-objects-java/" %}
