# External Store

1. Separation of Concerns(관심사의 분리)

- Input → Process → Output이란 3단계로 코드를 적절히 구분

  ```zsh
  Input: 프로그램 시작
  Process: 프로그램 초기화
  Output: 사용자에게 초기 UI 보여주기
  Input: 사용자의 입력
  Process: 사용자의 입력에 따라 처리
  Output: 처리 결과 보여주기
  Input: 사용자의 또 다른 입력
  …반복…
  ```

2. Flux Architecture

- FaceBook에서 MVC 대안으로 내세운 Architecture
  2-way binding으로 발생하는 복잡한 상황을 방지하기 위해사용
  unidirectional data flow 강조

  ```zsh
  Action → 이벤트/메시지 같은 객체.
  Dispatcher → (여러) Store로 Action을 전달. 메시지 브로커와 유사하다.
  Store (여러 개) → 받은 Action에 따라 상태를 변경. 상태 변경을 알림.
  View → Store의 상태를 반영.
  ```

- Redux 단일 store 사용

  ```zsh
    Action
    Store -> dispatch를 통해 Action을 받고,
    사용자가 정의한 `reducer`를 통해 State를 변경
    View -> State를 반영
  ```

- 3단계 프로세스

  ```zsh
    Input -> Action + dispatch
    Process -> reducer
    Output -> View(React)
  ```

3. External Store

- forceUpdate
  `상태가 바뀌면` 해당 component와 하위component를 re-rendering하기 때문에 `forceUpdate` 같은 기능이 필요

  ```zsh
  const [, setState] = useState({});
  const forceUpdate = () => setState({});
  ```

- 위의 코드를 커스텀 Hook으로 만들자

  ```zsh
  function useForceUpdate() {
    const [, setState] = useState({});
    return useCallback(() => setState({}), []);
  }
  ```

- React는 UI만 담당, 비즈니스 로직은 TypeScript가 담당(관심사의 분리)
  UI요소에 대한 테스트 대신, 오래 유지되는 비즈니스 로직에 대한 테스트 코드를 작성해 유지보수에 도움이 되는 테스트 코드를 치밀하게 작성할 수 있다.
