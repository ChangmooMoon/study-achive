# ES6 module

* module(export, import) 이해 - babel 설정이 필요함

```jsx
// dist/bundle.js
import { log } from './myLogger' // myLogger 파일이 객체의 형태로 넘어오기 때문에 destructing 형태로 log func만 뽑아서 쓴다

const root = document.querySelector('#root')
root.innerHTML = `<p>Hello world!</p>`

log()

// myLogger.js
export default function log(data) { // export default로 export. default는 이 파일 내에 유일한 export
	console.log(data)
}
```

* module(export, import) 기반 서비스 구현

```jsx
// bundle.js
import log, { getTime, getCurrentHour, MyLogger, _ } from './myLogger'

const root = document.querySelector('#root')
root.innerHTML = `<p>Hello world!</p>`

log('test 1234')
log(`now time is ${getTime()}`)
log(`current hour is ${getCurrentHour()}`)

const logger = new MyLogger()
log(`my lectures are ${logger.getLectures()}`)
_.log('hihi')
```

```jsx
// myLogger.js
// export default function log(data) {
// 	console.log(data)
// }

export const getTime = () => {
	return Date.now()
}

export const getCurrentHour = () => {
	return (new Date).getHours()
}

export default class MyLogger {
	constructor(props) {
		this.lectures = ['java', 'IOS']
	}

	getLectures() {
		return this.lectures
	}
}

/* utility */
export const _ = {
	log(data) {
		if(window.console) console.log(data)
	}
}
```
