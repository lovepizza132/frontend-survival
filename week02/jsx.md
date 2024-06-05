# JSX 사용해보자

## JSX

- JSX 정의
  `JSX`는 XML처럼 작성된 부분을 React.createElement를 쓰는 코드로 변환한다. 중괄호를 써서 JavaScript코드를 그대로 쓸 수 있고, 결국은 JavaScript 코드와 1:1로 매칭된다.

- 변환기 중 제일 유명한 Babel로 확인 가능
  <https://babeljs.io/repl>
  "Presets"에서 react를 체크하거나, Plugins에서 @babel plugin-transform-react-jsx를 추가하면 JSX를 실험할 수 있다.

- JSX와 ReactElement Tree 변환 예시

  ```zsh
  <div>
    <p>Count: {count}!</p>
    <button type="button" onClick={() => setCount(count + 1)}>Increase</button>
  </div>
  ```

  ```zsh
  React.createElement(
    "div",
    null,
    React.createElement("p", null, "Count: ", count, "!"),
    React.createElement("button", { type: "button", onClick: () => setCount(count + 1) }, "Increase")
  );
  ```

- React Element
  JSX 대신 createElement를 사용해 ReactElement 트리 갱신가능
  JSX Runtime은 _jsx란 함수를(import 안해도 됨), preact는 h란 함수를 지원

  ```zsh
  // Inserted by a compiler (don't import it yourself!)
  import {jsx as _jsx} from 'react/jsx-runtime';

  function App() {
    return _jsx('h1', { children: 'Hello world' });
  }
  ```
  
  ```zsh
  import { h } from 'preact';
  h(
    'div',
    { id: 'foo' },
    h('span', null, 'Hello!')
  );
  // <div id="foo"><span>Hello!</span></div>
  ```

- Virtual DOM
  Virtual DOM은 UI의 이상적인 또는 "가상"적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 "실제" DOM과 동기화하는 프로그래밍 개념-> 재조정 과정

  VDOM은 실제 DOM과 비교를 통한 변경사항을 DOM에 적용

- Virtual DOM 사용 이유
  VDOM을 쓰는 건 빠르고 유지보수가 가능하기 때문
  React의 선언적 API를 가능하게 합니다.

- StrictMode
  애플리케이션의 내의 잠재적인 위험을 찾기위한 도구
  `Fragment`와 같이 UI를 렌더링하지 않으며, 자손들에 대한 부가적인 검사와 경고를 활성화(개발모드에서만 활성화, 프로덕션 빌드에는 영향 X)

  ```zsh
  root.render((
    <React.StrictMode>
      <App />
    </React.StrictMode>
  ));
  ```
