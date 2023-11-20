**호출 스케줄링 scheduling a call ?**

함수를 즉시 실행하지 않고 일정시간이 지난 이후에 실행하기 위해 함수 호출을 예약하기위해

타이머 함수를 사용하는데 이를 호출 스케줄링 이라고 함

### Timer Function 타이머 함수

💡 JavaScript 에서는 `setTimeout` `setinterval` 이라는 두개의 타이머 함수와
타이머를 제거할 수 잇는 `clearTimeout` `clearInterval` 두개의 함수를 제공함

이들 모두 JavaScript 에서 지원하는 함수 객체가 아닌 브라우저와 Node.js 환경에서 제공하는 호스트 객체임

- JS 엔진은 싱글 스레드 동작이기 때문에 타이머 함수들은 비동기 처리 방식으로 동작하게됨

### setTimeout / clearTimeout

💡 두 번째 인자로 전달받은 시간을 기준으로 단 한 번 동작하는 타이머를 생성함

이후 시간이 만료되면 첫 번째 인자로 전달받은 `Callback Function`을 실행함

```jsx
const timer = setTimeout( Callback , delay , param1 , param2 … )
```

- `Callback`
  타이머가 만료된 후 호출될 콜백 함수
- `delay`
  타이머의 만료되기까지의 시간으로 기본값은 0
- `param..`
  Callback 함수에 전달해야하는 인수가 존재할 경우 전달할 수 있음

```jsx
clearTimeout(timer);
// clearTimeout 함수로 호출 스케줄링을 취소함
```

### setInterval / clearInterval

💡 모든 부분에서 Timeout 과 동일하지만 다른점은 한번만 실행되는것이 아니라 반복실행됨

두 번째 인수로 전달받은 시간마다 반복 동작하는 타이머를 생성하게됨

## 디바운스 & 스로틀

💡 두개의 개념 모두 scroll, resize 등의 짧은 시간 연속해서 발생하는 이벤트로 인한 성능 저하를 방지함

### 디바운스

짧은 시간 간격으로 이벤트가 발생하는 경우 Event Handler 를 호출하지 않다가

일정 시간이 경과한 이후에 마지막 데이터만 Event Handler 를 이용해 한 번만 호출되도록 함

```jsx
const debounce = (callback, delay) => {
  let timer;

  return (...args) => {
    if (timer) clearTimeout(timer);

    timer = setTimeout(callback, delay, ...args);
  };
};
```

- 주로 사용자의 텍스트 입력 필드에 값을 입력 받을때 자주 사용됨
- `Underscore` `Lodash` 라이브러리의 debounce 함수 사용을 권장함

### 스로틀

연속적으로 발생하는 Event 속에서 처음 Evnet가 발생하고 전달받은 일정 시간동안

호출이 무시되어 일정 시간 단위로 Evnet Handler가 호출되는 호출 주기를 만듬

```jsx
const throttle = ( callback , delay ) => {
	let timer;

	return (...args) => {
		if(timer) return);

		timer = setTimeout(()=>{
			callback(...arg)
			timer = null;
		},delay)
	}

}
```
