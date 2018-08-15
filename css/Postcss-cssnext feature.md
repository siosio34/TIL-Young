## Postcss-cssnext feature



#### custom properties & var()

- :root 태그에 커스텀 프로퍼티를 변수형태로 설정할 수 있음.

- 이렇게 설정된 커스텀 프로퍼티는 var() 을 이용해서 가져올수 있음.

  ```css
  :root {
    --mainColor: red;
  }
      
  a {
    color: var(--mainColor);
  }
  ```

#### custom properties sets & @apply

- properties 집합들을 @apply 태그를 사용해서 가져올 수 있음.

  ```scss
  :root {
    --danger-theme: {
      color: white;
      background-color: red;
    };
  }

  .danger {
    @apply --danger-theme;
  }
  ```

#### reduced calc()

- css 내에서 간단한 수식 가능

  ```scss
  :root {
    --fontSize: 1rem;
  }
      
  h1 {
    font-size: calc(var(--fontSize) * 2);
  }
  ```

#### custom media queries ranges

```scss
@media (width >= 500px) and (width <= 1200px) {
}

@custom-media --only-medium-screen (width >= 500px) and (width <= 1200px);

@media (--only-medium-screen) {
 
}
```



#### Custom selectors

```scss
@custom-selector :--button button, .button;
@custom-selector :--enter :hover, :focus;

:--button {
  
}

:--button:--enter {
  hover and focus styles 을 나의 버튼을 추가할
}
```



#### nesting

```scss
a {
  /* direct nesting */
  & span {
    color: white
  }
  /* @nest rule ( for complex nesting ) */

  @nest span & {
    color: blue
  }
  
}

/* result */
a {
 
}
a span {
  color: white
}
span a {
  color: blue
}
```



- :root ㅇ