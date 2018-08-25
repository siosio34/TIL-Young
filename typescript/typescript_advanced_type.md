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

### type alias 
```typescript
- 기존 타입에 새이름을 짓는다. 
- 일반적인타입(string ,number) 같은데 써서는 별 의미가 없고 유니언 타입이나 리터럴 타입 같은 다소 복잡한 타입에 사용하면 좋음.
ex) type User = {
	id: myId;
	alias?: myAlias;
	city: string;
}
```

### 제네릭
```typescript
- 타입스크립트의 꽃인기능. 이걸 잘 배워두면 리액트에서도 요긴하게 써먹을수 있다.
- 예를들면 액션 크리에이터 함수를 만든다하면 제네릭을 이용하면 해당 액션에 페이로드가 있든 없는 하나의 함수로 처리가능하게 만들수 있다. 
- 컴파일 시간에 타입 안정성을 보장한다.
- 캐스팅과 관련된 코드를 제거할수 있게된다.
- 제네릭을 이용하면 제네릭 로직을 이용해 재사용이 가능한 코드를 제작할 수 있음.

function arrayConcat<T(타입매개변수)>(string1: T(매개변수타입), string2: T) : T[](리턴형타입) {
	return array1 + array2; // 이건 컴파일 에러가 뜬다.
	return String(string1) + String(string2) // 이렇게 매개변수 T로 정해진경우 타입매개변수간의 연산이 지원하지않기때문에 그걸 방지하기위해선 아래와 같이 타입 캐스팅 코드를 써줘야한다. 
} 

- 매개변수에 넣은 T의 타입에 따라 나머지타입이 결정됨. 

- 그러면 타입캐스팅 코드를 추가없이 타입매개변수(T)간 연산을 할려면 어떻게 해야되는가? 

	1. 타입을 몇가지로 제한한다 . String type으로 제약하기위해 String type 을 상속해본다.
	-> <T extends string>
	-> <T extends string | number> (Union type도 가능하다.)
	
	근데 이번에도 타입매개변수간의 연산을 지원할 수 없다는 에러가 뜸
	
	2. 오버로드 함수를 이용해서 타입매개변수간의 연산을 구현한다.(정답)
	
	function concat<T>(strs: T, strs: T): T;
	function concat<T>(strs: any, strs2: any) {
		return strs + strs2;
	}
	
- 2개이상의 매개변수를 받는것도 가능하다.
function put<T, T2>(strs: T, strs2:T2) {}
그런데 개인적인 생각으로써는 그냥 매개변수 하나 쓰는데 그거를 유니온 타입으로 정의해서 쓰면 더 간단해질거같다.

- 룩업타입을 제네릭 클래스에 적용하기.
function getValue<T, K extends keyof T>(obj: T, key: K) {
	return obj[key];
}
let numbers = {one:1 ,two:2 ,three: 3};
console.log(getValue(numbers, "happy")) (x)
```

### 참고
- 타입스크립트 퀵스타트(도서)