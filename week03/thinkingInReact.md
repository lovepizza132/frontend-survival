### Thinking in react

1. Break the UI into a component hierarchy(컴포넌트 계층구조)
2. Step 2: Build a static version in React

- 데이터
  B/E에서 JSON 형태의 데이터를 돌려주는 API를 제공한다고 가정(대부분 REST API or GraphQL)

  - REST API
    GET, POST, PUT/PATCH, DELETE(CRUD)
    Resource 중심

  - GraphQL
    Graph 자료구조
    Query에서 얻고자 하는 걸 지정
    Query(READ), Mutation(Command: Create, Update, Delete), Subscription(Event)

  F/E는 이 데이터를 사용자가 볼 수 있도록 UI를 구성한다. React는 선언형으로 UI를 구성할 수 있다.

- 컴포넌트 계층 구조
  - React의 강력한 특징
    Component Based
    Build encapsulated components that manage their own state, then compose them to make complex UIs
  - 몇가지 기준
    SRP(Single Responsibility Principle) - `단일책임원칙`
    CSS 기준 활용
    Design's Layer
    Information Architecture(JSON Schema의 영향) -> 실제로 엄청 많이 쓰임, 자연스런 SRP를 위해 강제 됨

- Extract Function(함수 추출)
  - SRP를 위한 수단(변화-영향 범위의 크기를 제약)
  - 일단 길게 코드 작성 후, 적절히 자를 수 있는 부분이 보일 때 `함수로 추출`
  - 코드를 작성하기 어려운 상황에 직면했을 때 함수로 추출(다른 파일을 만들어야 한다고 생각하지 않아도 됨)
  - 컴포넌트 나누는 기준이 애매하면 다시 하나의 컴포넌트로 합치고(Inline Method) 다시 나눠도 됨

- Props
  - 컴포넌트를 연결하는 방법
  - 컴포넌트간 메시지를 주고받는 인자
