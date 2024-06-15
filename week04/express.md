# Express 개발환경 & REST API

- Express(간단한 서버 앱) 개발환경 세팅
  Node.js를 위한 빠르고 개방적인 간결한 웹 프레임워크

  - Express 설치 전 폴더 구성

    ```zsh
      mkdir express-demo-app
      cd mkdir express-demo-app
      touch .gitignore
      echo "/node_modules/" > .gitignore
    ```

  - 패키지 초기화

    ```zsh
      npm init -y
    ```

  - TypeScript 설치

    ```zsh
      npm i -D typescript
      npx tsc --init
    ```

  - ESLint 설치

    ```zsh
      npm i -D eslint
      npx eslint --init
    ```

  - ts-node 설치

    ```zsh
      npm i -D ts-node
    ```

  - Express 설치

    ```zsh
      npm i express
      npm i -D @types/express
    ```

- Express 예시
  TypeScript에 맞춰서 `app.ts`파일 작성

    ```zsh
      import express from 'express';

      const port = 3000;

      const app = express();

      app.get('/', (req, res) => {
        res.send('Hello, world!');
      });

      app.listen(port, () => {
        console.log(`Server running at http://localhost:${port}`);
      });
    ```

  - ts-node로 실행

    ```zsh
      npx ts-node app.ts
    ```

  - Express사용 시 코드 수정하면 서버 재실행이 필요 => nodemon으로 해결

    ```zsh
      npm i -D nodemon
      npx nodemon app.ts
    ```

- REST API(RESTful API)
  `Representational State Transfer` 아키텍처 스타일의 설계 원칙을 준수하는 API

- REST 제약 조건(6개)-
  - client-server(client/server 구조)
  - stateless(무상태성)
  - cacheable(캐시 처리 가능)
  - layered system(계층화 시스템)
  - code-on-demand(주문형 코드, optional)
  - uniform interface(인터페이스 일관성)

  출처: <https://velog.io/@dsa2341/REST-API-%EB%BD%80%EA%B0%9C%EA%B8%B0-6vpzm4ix>

- 대개 Resource와 HTTP Verb만 도입하는 수준으로 사용
  `/write-post` (X)
  `/posts` -> 뭔가를 한다(CRUD) (O)

- CRUD에 대해 HTTP Method를 대입. Read는 Collection(복수)과 Item(Element)(단수)로 나뉨.
  기본 리소스 URL: `/products`
  Read(Collection) -> `GET /products`
    상품 목록 확인
  Read(Item) -> `GET /products/{id}`
    특정 상품 정보 확인
  Create(Collection Pattern 활용) -> `POST /products`
    상품 추가 (JSON 정보 함께 전달)
  Update(Item) -> `PUT or PATCH /products/{id}`
    특정 상품 정보 변경(JSON 정보 함께 전달)
  Delete(Item) -> `DELETE /products/{id}
    특정 상품 삭제

- REST API 예제

  ```zsh
    app.get('/products', (req, res) => {

      const products = [
        {
          category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
        },
        {
          category: 'Fruits', price: '$1', stocked: true, name: 'Dragonfruit',
        },
        {
          category: 'Fruits', price: '$2', stocked: false, name: 'Passionfruit',
        },
        {
          category: 'Vegetables', price: '$2', stocked: true, name: 'Spinach',
        },
        {
          category: 'Vegetables', price: '$4', stocked: false, name: 'Pumpkin',
        },
        {
          category: 'Vegetables', price: '$1', stocked: true, name: 'Peas',
        },
      ];

      res.send({ products });
    });
  ```
