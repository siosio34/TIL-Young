## Jest

### toBe
- Object.is 함수를 사용해서 값이 같은지 판단한다. 
- Object의 값을 체크하고 싶으면 toEqual 함수를 사용한다.

```js
test('two plus two is four', () => {
	expect(2+2).toBe(4);
})

```

### toEqual 
- object 나 array 의 모든 요소 검사가능.

```javascript
test('object assignment', () => {
	const data = {one: 1};
	data['two'] = 2;
	expect(data).toEqual({one: 1, two: 2})
})
```

### Truthiness
- undefined, null, false 를 구별하고 싶을때도 있고 아닐때도 있다. jest 는 너가 원하는걸 도와줄 helper 함수들을 가지고 있다

```
- toBeNull -> null값일때
- toBeUndefined -> undefined 값일때
- toBedeined -> 위에랑 반대경우
- toBeTruthy -> if 안에 조건으로 들어갔을때 true 처리되는경우(ex 값이 있을경우, true, undefined, null 값이 아닌경우)
- toBeFalsy  -> toBeTruthy 와반대경우

```

### 숫자비교
- toBe, toEquel 다됨.
- 이상, 초과, 이하, 미만을 다루기 위한 함수들도 존재함.
	- toBeGreaterThan
	- toBeGreaterThanOrEqual
	- toBeLessThan
	- toBeLessThanOrEqual

### 문자열비교
- toMatch 사용하면 정규표현식 사용가능 개꿀개꿀

### 배열
- toContain 사용하면 요소검사가능

## 비동기코드 테스트
- callback, promise, async/await 등 여러방법이 있지만 난 asycn/await + resolve, rejects 같이쓰는게 좋은거 같으니 저것만할거임.
- expect.assertions 을 붙이지않으면 테스트가 실패하지않는다.
- expect.assertions(number) 특성수의 어설션이 호출되었는지 확인한다. 즉 비동기 처리구문이 하나면 number 은 1 두개면 number 은 2여야한다.

```js

```



## 출처
- https://jestjs.io/docs