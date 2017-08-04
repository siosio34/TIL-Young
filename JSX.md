### JSX

##### 참고자료 - https://velopert.com/867

- #### 장점

  - 컴파일링 되면서 최적화되므로 빠르다.
  - 컴파일 과정에서 에러감지가능

- #### 특징

  - 컴포넌트 안 여러 엘리먼트를 렌더링할때 필수적으로 container element안에 포함 시켜줘야됨.

    - ex ) - 안되는거

      ```jsx
      return (
        <h1> Hello World</h1>
        <h2> Welcome </h2>
      );
      ```

    - ex) - 바른 예

      ```jsx
      return  {
        <div>
          <h1> Hello World</h1>
        	<h2> Welcome </h2>
        </div>
      }
      ```

  - if else 문 사용이 불가능. -> condion ? true : false

  - 주석 작성시  { /* comments */ }

  ​