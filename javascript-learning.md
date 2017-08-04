- 자바스크립트에서 === 은 값뿐만아니라 타입과 형식이 같은지 비교한다.

- NaN 은 자기자신과 비교해도 false 이다.

- 해체할당

  ```javascript
  const obj = { b:2 , c:3, d: 4};

  // 해체 할당
  const {a, b, c} = obj;
  a; // undefined "a" 프로퍼티가 없음.
  b; // 2
  c; // 3
  d; //referenceError "d"가 정의되지않음.
  ```

- 확산 연산자

  ```javascript
  const arr = [1,2,3,4,5];

  let [x, y, ...rest] = arr;
  x; // 1
  y; // 2
  rest; // [3,4,5]
  ```

- 화살표 표기법

  ```javascript
  const f1 = function() { return "hello"; }
  const f1 = () => "Hello";

  const f2 = function(name) [ return "hello, ${name}";]
  const f2 = name => "hello, ${name}"

  const f3 = function(a, b) { return a + b; }
  const f3 = (a,b) => a+b;
  ```

  ​