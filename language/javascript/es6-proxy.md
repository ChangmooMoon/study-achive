# ES6 proxy

* Proxy로 interception 기능 구현
  * 어떤 object를 가로채서 추가로 다른 작업을 더하는 방식
  * `Proxy`는 특정 객체를 감싸 프로퍼티 읽기, 쓰기와 같은 객체에 가해지는 작업을 중간에서 가로채는 객체로, 가로채진 작업은 `Proxy` 자체에서 처리되기도 하고, 원래 객체가 처리하도록 그대로 전달되기도 함

```jsx
let proxy = new Proxy(target, handler)

target – 감싸게 될 객체로, 함수를 포함한 모든 객체가 가능합니다.
handler – 동작을 가로채는 메서드인 '트랩(trap)'이 담긴 객체로, 여기서 프락시를 설정합니다(예시: get 트랩은 target의 프로퍼티를 읽을 때, set 트랩은 target의 프로퍼티를 쓸 때 활성화됨).
proxy에 작업이 가해지고, handler에 작업과 상응하는 트랩이 있으면 트랩이 실행되어 프락시가 이 작업을 처리할 기회를 얻게 됩니다. 트랩이 없으면 target에 작업이 직접 수행됩니다.

const myObj = { name: 'mcm', changedValue: 0}

const proxy = new Proxy(myObj, {
	get: function(target, property, receiver) { // get트랩
		console.log('get value')
		return target[property]
	},
	set: function(target, property, value) { // set트랩
		console.log('set value')
		++target['changedValue'];
		target[property] = value
	}
})

proxy.name = 'hihi' // set value
console.log(proxy.name) // get value , hihi
```
