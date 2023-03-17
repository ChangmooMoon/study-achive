# scope, var closure 이슈, let, const

*   var 변수의 특징

    * **function level scope** - 함수의 코드 블록만을 스코프로 인정한다. 전역변수 외부에서 생성된 변수는 모두 전역변수이기 때문에 남용될 수 있다
    * var 키워드 생략 허용 - 암묵적인 전역변수가 허용된다
    * 변수 중복 선언 허용 - 의도하지 않는 변수값의 변경이 일어날 수 있다
    * **변수 호이스팅** - 변수를 선언하기 이전에 참조할 수 있다

    → let, const 사용
*   var의 closure 이슈

    * 대부분의 언어들은 블록 레벨 스코프를 따름
    * function-level scope: 함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉 함수 내부에서 선언된 변수는 지역 변수이며, 함수 외부에서 선언한 변수는 모두 전역 변수이다. (var)
    * block-level scope: 모든 코드 블록(function, if, for,while, try-catch...) 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다. 즉 코드 블록 내부에서 선언한 변수는 지역 변수이다. (let, const)

    ```jsx
    var list = document.querySelectorAll('li')
    for(var i = 0; i < 4; ++i) {
    	list[i].addEventListener("click", function() {
    		console.log(i + "번째 리스트입니다")
    	}) // 클릭하면 4 4 4 4 나옴
    }

    for루프의 i가 전역변수라서 4가 출력된다. 

    for(var i = 0; i < 4; ++i) {
    	(function (idx) {
    		list[idx].addEventListener('click', function() {
    			console.log(idx)
    		})
    	}(i))
    }

    IIFE로 작성할 수 있다(정의와 동시에 실행). var의 함수레벨 스코프로 인하여 for 루프의 초기화식에
    사용된 변수가 전역스코프를 가져서 발생하는 문제를 회피하기 위해 클로저를 이용함
    (클로저 - 반환된 내부함수가 자신의 선언됬을 때의 환경(lexical environment)인 스코프를 기억하여
    자신이 선언됬을 때의 환경(스코프) 밖에서 호출되어도 그 환경(스코프)에 접근할 수 있는 함수)

    for(let i = 0; i < 4; ++i) {
    	list[i[.addEventListener('click', function() {
    		console.log(i)
    	})
    }

    for루프의 let i 변수는 for루프에서만 유효한 지역변수이다. 하지만 for루프가 종료되어도 자유변수 i를 참조하는
    함수가 존재하면 계속 유지된다
    ```
* const - 상수. 재할당 불가
  * const list = \[’a’, ‘b’, ‘c’], list에 대해서 재할당 불가이지 list 내부 값 변경은 가능하다
  *   immutable array 구현

      ```jsx
      const list = ['a', 'b', 'c']
      list2 = [].concat(list, 'd')
      console.log(list === list2) // false
      ```
