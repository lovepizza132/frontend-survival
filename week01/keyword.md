### 핵심키워드

# JavaScript

  `JavaScript`는 정적인 `HTML`을 조작해 웹페이지를 다이나믹하게 바꿔준다.

# Node.js

  JavaScript의 런타임(실행 환경)
  `브라우저`에는 JavaScript의 해석 엔진이 있다.(과거 인터넷 브라우저로만 JavaScript 실행 가능)
  V8 엔진 기반의 `Node.js` 등장으로 브라우저 내에서의 환경이 아닌 다른 환경에서도 JavaScript 사용 가능
  노드 정의
    - 서버: 네트워크를 통해 클라이언트에 정보나 서비스를 제공하는 컴퓨터 또는 프로그램
    - 자바스크립트 런타임: 자바스크립트 프로그램을 컴퓨터에서 실행할 수 있게 해주는 환경

# npm(node package manager)

  `노드 패키지(modules)`를 관리하기 위한 매니저 시스템(설치, 업데이트, 삭제에 도움을 주는 툴)
  npm에서의 노드는 JavaScript의 런타임을 의미
  대부분의 JavaScript 프로그램은 패키지라는 이름으로 npm에 등록(찾아 설치 가능)

# node_modules

  실제로 설치된 의존성 모듈들이 모두 들어있는 디렉토리
  애플리케이션이 사용하는 코드는 여기서 쓰게된다.
  `package.json`정보를 바탕으로 `npm install`명령어로 node_modules 언제든지 추가

# package.json

  생성한 프로젝트의 `메타정보`와 프로젝트가 `의존하고 있는 모듈`들에 대한 정보(`version range` 포함)를 `json`형태로 모아놓은 파일
    - 외부 모듈들이 많아지면 관리가 어려워짐
    - 새로운 프로젝트에서 모듈들이 많다면 번거롭게 매번 npm 명령으로 설치해야 함
    - `npm init` 으로 package.json 초기 파일 생성
    - `npm install`할 때 기준이 되어주는 파일, 대략적인 의존성의 버전 관리

# package-lock.json

  프로젝트에 설치되어야하는 의존성의 정확한 버전을 관리해주는 파일
    - package.json 대략적인 범위 => ^4.10.3
    - package-lock.json 구체적인 범위 명시

# npx(Node Package eXecute)

  `npm 5.2.0`버전 이상부터 npm 설치 시, 자동으로 `npx` 설치
  npm을 더욱 편하게 사용할 수 있도록 도와주는 `도구`이다.
  패키지를 설치하지 않고도 npm 레지스트리에서 원하는 패키지를 실행(execute)할 수 있다. 즉, `npm package runner`로 npx는 일회용 패키지로써 사용.

# CommonJS VS ES Modules

  모듈 expoort와 import 방식
    `module.export`로 모듈을 내보내고 require()로 접근하는 CJS
      ```zsh
        // CJS 방법
        module.exports = { ... }        // 모듈 내보낼 때
        const utils = require('utils'); // 모듈 가져올 때
      ```
    `export`로 모듈을 내보내고 `import`로 접근하는 ESM
      ```zsh
        // ESM 방법
        export.default =()=> { ... }; // 모듈 내보낼 때
        import utils from 'utils';    // 모듈 가져올 때
      ```

# React

  웹 프레임워크, 자바스크립트 라이브러리의 하나로서 사용자 인터페이스를 만들기 위해 사용된다.

  1. Data Flow
    데이터 흐름이 한 방향으로만 흐르는 `단방향 데이터 흐름`
  2. Component 기반 구조
    독립적인 단위의 소프트웨어 모듈 의미
    기능, UI, 단위로 캡슐화해 재사용성 높다. -> 유지보수 관리 용이
  3. Virtual DOM(Document Object Model)
    DOM Tree 구조의 가상의 Document Object Model
    이벤트 발생 시 매번 Virtual DOM을 만들고, 다시 그릴 때 마다 DOM과 비교하고 전후 상태를 비교해, 변경이 필요한 최소한의 변경사항만 실제 DOM에 반영해, 앱의 효율성과 속도를 개선
  4. Props and State
    `Props`란 부모 컴포넌트에서 자식 컴포넌트로 전달해 주는 데이터
    `읽기 전용 데이터`로 props를 전달해준 최상위 부모 컴포넌트만 props 변경 가능

    `State`는 컴포넌트 내부에서 선언하며 내부에서 값을 변경할 수 있다.
    `동적인 데이터`, 사용자와의 상호작용을 통해 데이터를 동적으로 변경할 때 사용
    클래스형 컴포넌트에서만 사용할 수 있고, 각각의 state는 독립적이다
  5. JSX
    XML처럼 작성된 부분을 React.createElement를 쓰는 코드로 변환한다. 중괄호를 써서 JavaScript코드를 그대로 쓸 수 있고, 결국은 JavaScript 코드와 1:1로 매칭된다.

# React re-render

  React의 퍼포먼스를 신경쓸 때 2가지 사항 고려
    initial render: 컴포넌트가 화면에 처음 등장할 때
    re-render: 두 번째, 그리고 연이은 렌더링

  컴포넌트가 스스로 re-render하는 경우

  1. state 변화
    컴포넌트의 state 변경 시(보통 callback, useEffect hook에서 발생)
  2. 부모의 리렌더링에 의한 리렌더링
    부모 컴포넌트의 리렌더링되면 child도 리렌더링된다.
  3. context 변화
    Context Provider의 value가 변화될 때, 이 Context를 사용하고 있는 모든 컴포넌트 리렌더링
  4. hooks 변화
    hook 안에서 발생하는 것들은 해당 hook을 사용하는 컴포넌트에 속한다.
  5. props 변화
    memoization 되지 않은 컴포넌트에 대해서는 리렌더링에 있어 prop의 변화는 상관이 없다.
    `prop`이 변화하기 위해선 부모 컴포넌트에서 업데이트되어야 한다.
  6. IoC(Inversion of Control)
  