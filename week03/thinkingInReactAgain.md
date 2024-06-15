### Thinking in react again

3. Step 3: Find the minimal but complete representation of UI state
4. Step 4: Identify where your state should live
5. Step 5: Add inverse data flow

- React State
  - `변경`을 다루기 위한 요소
  - `Re-rendering`이란 주제에서 다뤄진다.
    `state`가 변경되면 해당 컴포넌트와 하위 컴포넌트를 다시 렌더링한다.
  - DRY(Don't Repeat Yourself)
  - SSOT(Single Source of Truth)

- React State의 조건
  - 변경돼야 한다.
    변경되지 않는 건 state로 다룰 가치가 없다.
  - 부모 컴포넌트가 props를 통해 전달하면 state가 아니다
  - 다른 state나 props를 이용해 계산 가능하다면 state가 아님

- Inverse Data Flow
  - 하위 컴포넌트의 props로 함수를 전달(콜백 함수)
  - TypeScript는 함수가 일급 객체 즉, 어떤 함수를 다른 함수에 인자로 넘겨주거나, 어떤 함구를 리턴값으로 사용할 수 있다.
  (익명 함수, 클로저 등과 함께 사용하면 시너지 큼)
  - useState를 이용해 구현
      state(상태)를 나타는 변수와 setState(해당 변수의 값을 변경하는 함수)를 Props를 통해 하위 컴포넌트로 전달
      하위 컴포넌트에서는 이벤트 발생 시 setState()를 호출하여, 상위 컴포넌트에 있는 state변수의 값을 변화시킬 수 있다.
