# TypeScript를 사용해서 redux의 타입 안정성 개선하기

## 함수의 action creator type 을 정의하는법

### 필요한이유
- type safe 한 reducer 모듈 제작
- handling side effect redux-observable or ngrx/store(angular)

### Typescript 2.8 이전 

1. 제일 먼저 액션타입을 정의한다.
2. 다음으로 액션 크리에이터 타입을 먼저 정의해야만한다. 
3. 정의한 두 타입을 가지고 액션 크리에이터를 정의한다.

```typescript
const ADD_TODO = '[TODO] ADD_TODO'
const AddTodoAction = { type: typeof ADD_TODO, payload: string }
const addTodo = (title: string): AddTodoAction => ({ type: ADD_TODO, payload: title})

- addTodo 의 내용이 바뀌거나 AddTodoAction 의 내용이 바뀐다고 가정하면 둘중 하나만 바껴도 전체적으로 수정을 해야됨.
- action creator 를 정의할때 그 타입을 먼저 정의하는것을 강제되서 코드가 길어짐.

```
### Typescript 2.8 이후
- ReturnType<T>: 함수형 타입의 리턴타입을 반환받을수 있음. 즉 함수의 정의로부터 return type을 반환받는게 가능해짐.

이를 이용하여
1. 제일 먼저 액션타입을 정의한다
2. 바로 액션크리에이터 정의가 가능하다.
3. 그리고 이 액션크레이터를 이용하여 바로 ReturnType을 통헤 타입을 정의가능하다.

```typescript
const ADD_TODO = '[TODO] ADD_TODO'
conset addTodo = (title: string) => ({type: ADD_TODO as type of ADD_TODO, paylaod: age })
const AddTodoAction = ReturnType<typeof addTodo>

typeof ADD_TODO 를 하지않으면 AddTodoAction 의 type 이 [TODO] ADD_TODO 가 아니라 string으로 변환되서 들어가게됨.
```

### 추가적인 모듈을 이용해서 boilerplate 줄이기.

##### action-helpers.ts
```typescript
export interface Action<T extends string> {
	type: T
}
export interface ActionWithPayload<T extends string, P> extends Action<T> {
	payload: P
}
export function createAction<T extends string>(type: T): Action<T>
export function createAction<T extends string, P>(type: T, payload: P): ActionWithPayload<T, P>
export function createAction<T extends string, P>(type: T, payload? P) {
	return payload === undefined ? { type } : { type, payload }
}
// 타입스크립트 정의 부분과 구현부분을 나누어놓음. 타입스크립트는 컴파일하게되면 interface 구문은 다 날아가게됨.
// payload? P 인 이유는 payload가 undefined 이 될수도 있는 부분이라 저런식으로 처리를 해주지 않으면 strict null check mode 일때 에러가 뜨게됨.
```
##### types.ts
```typescript
type FunctionType = (...args: any[]) => any
type ActionCreatorMapObject = { [actionCreator: string]: FunctionType }
export type ActionsUnion<A extends ActionCreatorMapObject> = ReturnType<A[keyof A]>
```
##### action.ts
```typescript
import { ActionsUnion } from './types'
import { createAction } from './action-helpers'

export enum ActionTypes {
	 const SET_AGE = '[core] set age'
	 const RELOAD_URL = '[router] Reload page'
}


export const Actions = {
	setAge: (age: number) => createAction(ActionTypes.SET_AGE, age),
	reloadUrl: () => createAction(ActionTypes.RELOAD_URL)
}

export type Actions = ActionsUnion<typeof Actions>
```
##### reducer.ts
```typescript
import * as fromActions from './actions'

export interface State {
	user: {age: number; name: string} | []
	reloadPage: boolean
}
export const initialState: State = {
	user: {},
	reloadPage: false
}

export const reducer = (state = initialState, action: fromActions.Actions): State => {
	switch(action.type) {
		case fromActions.SET_AGE: {
			const { palyload: newAge } = action

			const newUser = { ...state.user, age: newAge }
			const newState = { ...state, user: newUser }
			return newState
		}
		case fromActions.RELOAD_URL: {
			const { payload } = action // 이 부분을 작성하면 에러가 뜨게됨. 해당 action 은 payload가 없다는걸 사전에 정의함.
			return {
				...state,
				reloadPage: true
			}
		}
	}
}

// 앞서 정의했던 action 파일 내에서의 처리때문에 자동완성과 type check를 통한 에러 방지를 모두 지원가능
// 라이브러리를 이용한 방법은 아래 참고에 첫번째 url을 참고하면됨.
```


## 참고

- [react-redux-typescript-guide](https://github.com/piotrwitek/react-redux-typescript-guide) : 라이브러리를 사용하는 방법.
- [Improved Redux type safety with TypeScript 2.8](https://medium.com/@martin_hotell/improved-redux-type-safety-with-typescript-2-8-2c11a8062575) : 직접 구현하는방법
