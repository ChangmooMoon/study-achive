# 자주 쓰는 ES6 문법 정리

1. 기본적인 ES6 Desstructing assingnment 구조 분해 할당

```jsx
[a, b] = [10, 20] // [10, 20]
[a, b] = [b, a]; // 변수 swap. [20, 10]

[a,b, ...rest] = [10, 20, 30, 40, 50]
console.log(rest) // [30, 40, 50]

const person = {
    name: 'Ellery Moon',
    familyName: 'Moon',
    givenName: 'Ellery'
    company: 'goodgood company',
    address: 'Seoul',
}

const { familyName, givenName } = person; // 객체에서 필요한 Key-value 엔티티만 꺼내 씀

// 객체 생성시 키 생략하기
const name = 'Ellery moon';
const company = 'goodgood company';
const person = { // 객체를 생성할 때 프로퍼티 키를 변수 이름으로 생략할 수 있음
  name,
  company
}
```

2. 배열 loop를 함수형으로 작성

```jsx
let sum = 0;
for(int i = 5; i < 10; ++i) {
	sum += i;
}

const sum = Array.from(new Array(5), (_, k) => k + 5).reduce((acc, cur) => acc + cur, 0);
```

3. 중복 제거 Set, spread syntax (...)

```jsx
const names = ['Lee', 'Kim', 'Park', 'Lee', 'Kim'];
const uniqueNamesWithArrayFrom = Array.from(new Set(names);
const uniqNamesWithSpread = [...new Set(names)];
```

4. Spread syntax(...)를 이용한 객체 병합

```jsx
const person = {
	name: 'Ellery Moon',
	familyName: 'Moon',
	givenName: 'Ellery'
}

const home = {
    name: 'pangyo',
    address: 'Seoul'
};

const MCM = { ...person, ...home };
/ {
//   address: 'Seoul'
//   familyName: 'Moon'
//   givenName: “Ellery”
//   name: 'pangyo' // **중첩되는 키는 마지막에 대입된 값으로 정해진다.**
// }
```

4. &&, || 활용

```jsx
const name = participantName || 'Guest'; // ||: default value 넣어주고 싶을 때 사용
// participantName이 0, undefined, 빈 문자열, null일 경우 'Guest'로 할당

flag && func(); /// && flag가 true일 경우에만 실행

const getCompany = (address) => { // 객체 병합에도 응용할 수 있음
  return {
    name: 'pangyo',
    ...address && { address: 'Seoul' }
  }};
console.log(getCompany(false)); // { name: 'pangyo' }
console.log(getCompany(true)); // { name: 'pangyo', address: 'Seoul'}
```

5. 비구조화 할당 사용하기

```jsx
const makeContract = ({ name1, name2, contractName }) => { // 함수에 객체를 넘길 경우 필요한 것만 꺼내 씀
  return {
    name1,
		name2,
    contractName
  }
};
const Contract = makeContract({ name1: 'Ellery', name2: 'goodgood company', contractName: 'stock-option' });
```

6. 동적 속성

```jsx
const nameKey = 'name';
const emailKey = 'email';
const person = {
  [nameKey]: 'Ellery',
  [emailKey]: 'Ellerymoon@gmail.com'
};
```

6. !! 연산자: 0, null, '', undefined, NaN 값을 검사할 수 있음

```jsx
function check(variable) {
  if (!!variable) { // 0, null, '', undefined, NaN이 들어오면 여길 통과할 수 없음
    console.log(variable);
  } else {
    console.error('잘못된 값');
  }
}
```

{% embed url="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment" %}

{% embed url="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from" %}

{% embed url="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax" %}
