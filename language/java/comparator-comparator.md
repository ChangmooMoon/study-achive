# Comparator, Comparator

1. java.lang.**Comparable 인터페이스** - 이 인터페이스를 구현하는 객체 스스로에게 부여하는 한가지 기본 정렬 규칙을 설정한다

* Comparable을 구현하고 있는 클래스들은 같은 타입의 인스턴스끼리 서로 비교할 수 있는 클래스이다. (wrapper 클래스, String, Date, File…). 기본 정렬 기준을 구현하는 데에 사용한다.
* 인터페이스 내의 **int compareTo(T o) 메서드**는 객체 자기 자신(this)와 매개변수 객체 o를 비교한다. 두 객체가 같으면 0, 비교하는 값보다 작으면 음수, 크면 양수를 반환한다
* 기본적으로 오름차순으로 정렬되는데, 내림차순 or 다른 기준에 따라 정렬하고 싶으면 Comparator를 구현해서 정렬기준을 제공할 수 있다.

```java
class Student implements Comparable<Student> {
		int kor, eng, math;

    public Student(int kor, int eng, int math){
        this.kor = kor;
        this.eng = eng;
        this.math = math;
    }
		
		// base. 국어 점수 기준으로 오름차순 방식
		@Override
		public int compareTo(Student student) {
			if(this.kor > student.kor) return 1;
			else if(this.kor > student.kor) return -1;
			return 0;
		}
		
		// // simple. 1보다 간단한 방식
		@Override
		public int compareTo(Student student) { 	
			return this.kor - student.kor; // 내림차순으로 정렬한다면 student.kor - this.kor를 반환하면 된다
		}
}

// 실전. 객체의 여러 필드값에 대해서 각각 다른 정렬규칙을 적용
class Student implements Comparable<Student> {
    int kor, eng, math;

    public Student(int kor, int eng, int math){
        this.kor = kor;
        this.eng = eng;
        this.math = math;
    }

    @Override
    public int compareTo(Student student) {
        if(this.kor == student.kor)	     // 국어 점수가 일치한다면
            return this.eng - student.eng;  // 영어 점수를 기준으로 오름차순 정렬합니다.
        return this.kor - student.kor;      // 국어 점수가 다르다면, 오름차순 정렬합니다.
    }
};
```

2. java.util.**Comparator 인터페이스** - 정렬 대상 클래스의 코드를 직접 수정하지 못할 경우 사용한다.

* 기본 정렬 기준 외의 다른 기준으로 정렬하고자 할 때 사용
* Comparator 인터페이스의 구현체를 Arrays.sort()나 Collections.sort() 같은 정렬 메서드의 추가 인자로 넘긴다.
* 인터페이스 내의 **int compare(T o1, T o2) 메서드**는 두 매개변수 객체를 비교한다.
* Comparator를 익명 클래스, 람다표현식으로 대체할 수 있다.
* Stream으로 컬렉션이나 배열을 읽고 sorted() 메서드로 Comparator 구현체를 받아서 정렬한 뒤 새로운 리스트를 생성할 수도 있다.

```java
// 방법2. comparator 인터페이스 구현 - 람다함수로 대체할 수 있다. 
Arrays.sort(student, (a, b) -> a.kor - b.kor);

// String 내에 정의된 대소문자 구분 없이 사전순 정렬하는 Comparator
Arrays.sort(strArr, String.CASE_INSENSITIVE_ORDER);

Arrays.sort(students, new Comparator<Student>() {
	@Override
	public int compare(Student a, Student b) { // base.
		return a.kor - b.kor;
	}

	@Override
	public int compare(Object o1, Object o2) { // Comparable 구현하지 않은 객체를 오름차순으로 정렬
			if(o1 instanceof Comparable && o2 instanceof Comparable) {
				Comparable c1 = (Comparable)o1;
				Comparable c2 = (Comparable)o2;
				return c1.compareTo(c2) * -1; // 기본 정렬방식의 역으로 변경
			}
			return -1;
	}
});

// Stream으로 새로운 정렬된 객체를 반환하는 방식
// Stream 클래스의 sorted() 메서드는 Comparator 객체를 인자로 받아서 정렬기준으로 사용한다. 
List<Student> sortedList = list.stream().sorted((a, b) -> b.kor - a.kor).collect(Collectors.toList());
```
