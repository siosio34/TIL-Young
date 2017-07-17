## Constraint Layout(제약 레이아웃)

#### 개요

안드로이드 스튜디오 버젼 업글레이드를 하면서 기본 레이아웃이 Relative Layout 에서 Constraint Layout로 변경되었다. 요새 swift 로 ios 프로그래밍을 하다가 오랜만에 버젼업을 한 나로써는 처음보는 레이아웃이었다. 대체 무슨 장점이 있길래 안드로이드 스튜디오에서  레이아웃을 생성할때 지정된  default layout 이었던 Relative layout 을 Constraint Layout 로 변경이 되었는지 한번 알아보고 그걸 정리하게 되었다.



#### Constraint Layout가 무엇일까?

- 쉽게 말해서 강력해진 Relative Layout 이라고 생각하면 편하다. 기존 Relative Layout 은 각 요소들을 toRightOf, toLeftOf, toTopof,toBottomof 와 같은 걸 사용해서 요소들이 나타낼 위치를 정하게 된다. Constraint Layout 은 이것보다 훨씬 더 유연하고 많은 위치속성을 제공할 뿐만 아니라 정렬될 것인지도 정할수 있다. 

  ##### Constraint Layout 위치 제약조건

  - layout_constraintLeft_toLeftOf
  - layout_constraintLeft_toRightOf
  - layout_constraintRight_toLeftOf
  - layout_constraintRight_toRightOf
  - layout_constraintTop_toTopOf
  - layout_constraintTop_toBottomOf
  - layout_constraintBottom_toTopOf
  - layout_constraintBottom_toBottomOf
  - layout_constraintBaseline_toBaselineOf
  - layout_constraintStart_toEndOf
  - layout_constraintStart_toStartOf
  - layout_constraintEnd_toStartOf
  - layout_constraintEnd_toEndOf

  ​

#### Constraint Layout 장점

- 중첩된 뷰를 줄여서 성능을 향상할 수 있다.

  - 복잡한 화면의 안드로이드 UI 를 개발할때 각종 Linear, Relative Layout 에 중첩해서 사용하는 경우를 많이 겪었을 것이다. 하지만 이 레이아웃은 각 요소마다 위치속성 및 정렬기준을 정할 수 있어서 중첩된 뷰를 많이 줄여 xml 코드를 직관적이게 만들뿐만 아니라 성능도 향상된다.

  - 개발자 직강에 의해면 RelativeLayout과 ConstraintLayout 안에 동일한 레이아웃들을 넣는다면 ConstraintLayout의 성능이 동일하거나 더 좋다고 확신하다고 말할정도로 성능이 향상된다고 한다.

    ​

- 반응형 UI를 쉽게 만들수 있다.

  실제 IOS 프로그래밍 할때도 여러가지 제약조건을 통해 어떠한 기기에서도 일정한 화면을 보여주는 반응형을 쉽게 제작할 수 있다. 안드로이드에서도 Constraint Layout 사용하면 반응형을 쉽게 제작할 수 있다.

   https://androidkor.blogspot.kr/2017/02/constraintlayout-ui.html - Constraint Layout으로 반응성 UI 만들기 번역

  ​

#### 환경설정

Android Studio 2.3

1. ##### build.gradle에 아래 코드 추가

   ``` java
   compile 'com.android.support.constraint:constraint-layout:1.0.1'
   ```

2. ##### xml 파일에 기존 루트태그를 android.support.constraint.ConstraintLayout 교체.

   ```xml
   <!-- activity_main.xml -->
   <?xml version="1.0" encoding="utf-8"?>
   <android.support.constraint.ConstraintLayout
       xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:app="http://schemas.android.com/apk/res-auto"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       tools:context="com.dragon4.owo.resight_android.MainActivity">
     
   </android.support.constraint.ConstraintLayout>
   ```



#### 예제



#### 이 글을 마치며

- 직접 써본 결과 ios 프로그래밍을 할때 storyboard 로 화면을 구성하는 과정에서 쓰이는 제약추가하는 기능이랑 정말 똑같다. ios 프로그래밍을 하다가 오신분들은 생각보다 쉽게 이 레이아웃을 사용할 수 있고 이 레이아웃에 익숙해진 안드로이드 개발자도 나중에 ios 프로그래밍에서 화면을 제작할때 편할거라 생각된다. 
  ​

- 중첩된 뷰를 만들 필요가 적어서 이 레이아웃으로 화면을 제작했을대 훨씬더 xml 코드가 간단해져서 보기좋다.
  ​

- 이미 다른 레이아웃으로 만들어서 이 레이아웃에 관심이 없을수도 있다. 하지만 안드로이드 스튜디오에서 기존레이아웃을 Constraint Layout으로 변환해주는 툴도 제공한다. 
  ​
  방법은 https://androidkor.blogspot.kr/2017/02/constraintlayout-ui.html 이 사이트에 Convert Layout 목차에 보면 있다.!
  ​

- 처음 제약 설정할지 잘 모르겠는 사람들을 위해서 아래 화면에 노란색 별버튼을 누르면 안드로이드 스튜디오 내에서 알아서 제약을 걸어준다.
  ​
  ![](https://ww4.sinaimg.cn/large/006tKfTcgy1fdfinjubuyj30t20pgq4v.jpg)

- 이번 패치인지 저번 패치인지는 모르겠지만 안드로이드 스튜디오 디자인툴에 성능 및 기능이 많이 늘어났다. 원래 코딩으로만 화면을 구성하였는데 충분히 사용해볼만 한것 같다.

  ​

- 다른 참고자료들 보면 영상이나 사진도 많으니 꼭 한번 참고해보는걸 추천한다.



#### 출처 및 참고자료

https://realm.io/kr/news/aw207-android-constraint-layout-auto-value-extensions/

https://androidkor.blogspot.kr/2017/02/constraintlayout-ui.html

https://developer.android.com/training/constraint-layout/index.html

https://codelabs.developers.google.com/codelabs/constraint-layout/index.html?index=..%2F..%2Findex#0

