## 타입스크립트 Advanced

### 익명 함수의 함수 타입할당
```typescript
이렇게 지정하면은 구현체랑 타입선언이 같이 있어 형태가 보기좋지않음.

let myConcat = function (str1: string, str2: string) : string {return str1 + str2}

그래서

let myConcat: (str1: string, str2: string) => string = (str1, str2) => {return str1 + str2;};

이렇게 함수 타입과 구현체를 분리하는 방법을 쓰면 좋음.

익명 함수의 타입을 함수타입으로 분리하면은 반복적으로 재활용도 가능
type calcType = (a: number, b: number) => number;
let addCalc: calcType = (a,b) => a+b
```

### 인터페이스
```typescript
- es6 가 지원하지 않는 타입스크립트만의 특징
- 컴파일 후에는 깔끔하게 사라짐(그래서 성능에 영향을 미치지않는다.)

- 인터페이스를 배열 타입으로 지정하는법
interface Person {
	name: string;
	city: string;
}
let person: Person[] = [
	{ name: "a", city: "seoul" }
]
=> 이런식으로 지정하면 지정한 키값과 value 값은 string형식으로 사용해야함.
```

### readonly 제한자
```typescript
- const 랑 다른점.
1. const 와 달리 초기화를 강제하지않음.
2. 변수를 상수로 강제하긴하나 컴파일 시점까지만 유효
3. 기본적으론 재할당이 불가능 하지만 타입 aliasing 을 하게되면 가능해짐

```
### 참고
- 타입스크립트 퀵스타트(도서)