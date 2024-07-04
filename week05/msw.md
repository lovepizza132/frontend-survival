# MSW

- 코드 레벨이 아닌 네트워크 레벨에서 가짜를 구현
- 오프라인 작업 등을 지원하기 위한 서비스 워커의 기능을 유용히 활용한 것

1. MSW 패키지 설치

  ```zsh
  npm i -D msw@0.36.4
  ```
  
  setupTestts.ts 파일
    ```zsh
    import server from './mocks/server';

    beforeAll(() => server.listen({ onUnhandledRequest: 'error' }));

    afterAll(() => server.close());
    afterEach(() => server.resetHandlers());
    ```

  jest.config.js의 setupFilesAfterEnv에 설정
    ```zsh
    setupFilesAfterEnv: [
      '<rootDir>/jest-setup.js.ts',
      // '@testing-library/jest-dom',
      '<rootDir>/src/setupTestts.ts',
    ],
    ```

2. fetch-polyfill(github)

- node에서는 fetch가 사용되지만 브라우저에서 사용이 안되는 경우

  ```zsh
  npm i -D whatwg-fetch
  ```

- setupTestts.ts에 추가

  ```zsh
  import 'whatwg-fetch'
  ```

3. mocks

- server.ts구성

  ```zsh
  /* eslint-disable import/no-extraneous-dependencies */
  import { setupServer } from 'msw/node';
  import handlers from './handlers';

  const server = setupServer(...handlers);

  export default server;
  /* eslint-enable import/no-extraneous-dependencies */
  ```

- handlers.ts 구성

  ```zsh
  /* eslint-disable import/no-extraneous-dependencies */
  import { rest } from 'msw';
  /* eslint-enable import/no-extraneous-dependencies */
  import fixtures from '../../fixtures';

  const BASE_URL = process.env.API_BASE_URL || 'http://localhost:3000';
  const handlers = [
    rest.get(`${BASE_URL}/products`, (req, res, ctx) => {
      const { products } = fixtures;

      return res(
        // Ctx.status(200),
        ctx.json({ products }),
      );
    }),
  ];

  export default handlers;
  ```
