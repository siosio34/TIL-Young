**CSS** **Modules** - https://glenmaddern.com/articles/css-modules

1. CSS 문제점

   ​

   ![](http://ww3.sinaimg.cn/large/006tNc79gy1fhfvnhnxr1j30fz0c0aak.jpg)

2. 잘 정의된 기존 css 의 예제

   ![](http://ww3.sinaimg.cn/large/006tNc79gy1fhfvtt22pvj30lc05ht99.jpg)

   - Button 이라는 클래스의 이름이 중복적으로 사용.
   - 비록 명료하고 유지보수하기 쉬운 코드이기는 하나, 이름 규약을 짓는데 많은 노력이 들어감.

3. css Modules 를 사용했을때 예

   ![](http://ww2.sinaimg.cn/large/006tNc79gy1fhfvvx2eijj30kj03cglw.jpg)

   - Button 이라는 공통적 요소 제외 -> 이미 파일명이 submit-button.css 라서 굳이 그럴 필요가 없었음.
   - CSS Modules 는 실제로 불필요한 모든 지역 변수들의 prefix 를 추가해줘야 하는 css 문제점을 해결.

4. 사용법

   ![](http://ww1.sinaimg.cn/large/006tNc79gy1fhfwambkmhj30k202twep.jpg)

   - 네이밍 규약은 camelCase 사용
   - 리액트 예제

   ![](http://ww2.sinaimg.cn/large/006tNc79gy1fhfwff9vqij30k50bpgmv.jpg)

   - 복합적으로 사용하고 싶을때 - 정의해놓은 뒤 composes 요소를 사용

     ![](http://ww3.sinaimg.cn/large/006tNc79gy1fhfwhl57jjj30jp0ay74v.jpg)

     ​

5. 외부 파일을 참조하고 싶을때 - from 키워드 + composes 모듈로 외부 참조

   ![](http://ww3.sinaimg.cn/large/006tNc79gy1fhfwvuwh37j30k8097q3f.jpg)

