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

### 유니언 타입
```typescript
- 2개 이상의 타입을 하나의 타입으로 정의한것이다.
- 타입A | 타입B 형식으로 선언.
- 매개변수를 타입별로 나눠서 작업할때 유용하게 사용됨.
- 매개변수가 유니언 타입일때 안전한 값을 할당할려면 타입 검사를 거쳐 매개변수를 받아야함.

 EX) 적용하지 않았을때
function myIndexOf(x: number | string, y: string) {
	return x.indexof(y) // 여기서 오류가난다.
}
```

### 문자열 리터럴 타입
```
- 사용자가 타입에 정의한 문자열만 할당받을수 있게 하는 타입이다.

type EventType = "keyup" | "mouseover";

- 저렇게 표기하면 keyup 이라는 string  과 mouseover 이라는 string 밖에 할당하지 못한다.
- 리액트에서 액션에 타입안정성을 보장할때 쓰면좋다.
```

### lookup 타입
``` typescript
- keyof 를 통해 타입 T 의 하위타입을 생성해낸다.
- interface 랑 같이 쓰면 코드 깔끔히 작업가능.

interface Profile {
	name: string;
	gender: string;
	age: number;
}

type Profile1 = keyof Profile;
let pValue1: Profile1 =  "name" (o)
let pValue1: Profile1 =  "name2" (x)

type Profile2 = keyof Profile[];
let pValue1: Profile2 =  "length" (o)
let pValue1: Profile2 =  "push" (o)

type Profile3 = keyof Profile["name"];
let pValue1 = "length" (o)
let pValue1 = "length" (x)
```

### 참고
- 타입스크립트 퀵스타트(도서)