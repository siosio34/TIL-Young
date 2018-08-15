### Redux 정리

- 앱의 상태는 전부다 store에 있는 객체 트리에 저장.
- API로는 subscribe, dispatch, gestate 가 있다.
  - subscribe - store 에 정보가 업데이트 되는걸 구독, 뷰레이어에 바인딩
  - dispatch - 내부 store 의 상태를 변경함.
  - getstate - 현재 상태를 가져옴
- Redux 의 3가지 원칙
  - 어플리케이션의 모든 상태는 하나의 스토어 안에 하나의 객체트리 구조로 저자됩니다.
  - 상태는 읽기전용 - 상태를 변화시키는 방법은 액션객체를 전달하는것이 유일함.
  - 변화는 순수 함수로 작성되어야한다. - 액션에 의해 상태트리가 어떻게 변화하는 지를 지정하기 위해선 순수 Reduxer을 작성해야한다.



- 참고자료
  - https://deminoth.github.io/redux/
  - https://github.com/xgrommx/awesome-redux
  - https://github.com/reactjs/react-redux