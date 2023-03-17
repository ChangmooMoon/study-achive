# DTO vs VO



* DTO, VO를 혼동해서 쓰게 된 원인은 core J2EE 관련 책에서 VO라고 했다가 TO로 정정하게 됨. 이후 D 데이터를 붙여 DTO라고 칭하게 됨
* **DTO : 데이터 전달용, VO : 값 자체 표현용**
* DTO - Data Transfer Object
  * 계층간 데이터를 전달하기 위해 사용하는 객체 ex) Controller ↔ Service 레이어 간 데이터 전달
  * 오직 getter, setter만 가지고 다른 로직은 갖지 않는다.
  * setter를 사용하지 않고 생성자로 객체 초기화를 강제하면 전달 과정 중에서의 데이터 불변성을 보장할 수 있어서 더욱 안정적이다. (setter 존재 시에는 가변적, 없으면 불변)
  * **속성값이 모두 같다고 해서 같은 객체가 아니다**
* Entity 클래스
  * 데이터 베이스와 매핑되어 있는 핵심적인 클래스. 이 클래스를 기준으로 테이블이 생성되고 스키마가 변경됨.
  * 만약 이를 이용해서 요청, 응답값을 전달하는 클래스로 이용하게 되면 뷰가 수정될 때마다 엔티티 클래스도 변경해야됨. 엔티티와 연관된 다른 기능들에 영향을 미치게 되므로 대신 DTO를 사용해야 한다.
  * 응답값으로 여러 테이블을 조인한 결과를 사용하는 경우가 있기 때문에 엔티티 클래스와 뷰 결과값이 담긴 DTO를 분리해서 사용해야 한다.
* **VO - Value Object**
  * 값 그 자체를 표현하는 객체 ex) 돈 지폐에는 각각의 고유번호가 있지만 같은 가치를 가지고 값으로만 비교된다. (객체의 hashcode가 다르지만, 내부에 들어있는 필드값은 같을 수 있다)
  * 속성값이 모두 같으면 같은 객체이다.
*   HashXXX(HashSet, HashMap, Hashtable)의 동등비교 방식

    ![Screenshot 2023-02-06 at 10.56.21 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ddedcec5-5fd7-495c-bbb7-ec68767c663b/Screenshot\_2023-02-06\_at\_10.56.21\_PM.png)

    * hashCode() 값과 equals() 값이 모두 같아야 동등 객체이므로 완전한 VO로 만들기 위해서는 객체를 속성값으로만 비교하도록 equals(), hashCode()를 모두 오버라이딩 해줘야 한다.

```java
public class Money {
	private final int value;

	public Money(int value) {
		this.value = value;
	}
 
	public int getHalfValue() { // VO는 getter setter 이외의 로직을 가질 수 있다
		return value / 2;
	}

	@Override
	public boolean equals(Object o) {
		if (this == o) {
			return true;
		}
		if (!(o instanceof Money)) {
			return false;
		}
		Money money = (Money) o;
		return value == money.value
	}

	@Override
	public int hashCode() {
		return Objects.hash(value);
	}

}
```

[\[10분 테코톡\] 📍인비의 DTO vs VO](https://youtu.be/z5fUkck\_RZM)

{% embed url="https://doing7.tistory.com/79" %}

{% embed url="https://cheese10yun.github.io/lombok/" %}
