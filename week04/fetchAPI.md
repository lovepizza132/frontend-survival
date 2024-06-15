# Fetch API

- 기본적인 사용법

    ```zsh
      fetch('http://localhost:3000/products');
      // → Promise

      await fetch('http://localhost:3000/products');
      // → Response

      const response = await fetch('http://localhost:3000/products');
      // → response.body는 ReadableStream

      const reader = response.body.getReader();

      const chunk = await reader.read();
      // → chunk.value는 Uint8Array 타입.
      // → 원래는 chunk.done이 true일 때까지 반복해야 한다.

      const body = new TextDecoder().decode(chunk.value);

      const data = JSON.parse(body);
      JSON을 기본 지원한다.

      const response = await fetch('http://localhost:3000/products');
      const data = await response.json();
    ```

  - 다른 HTTP Method를 쓰고 싶다면?

      ```zsh
        const response = fetch(url, {
          method: 'POST'
        });
      ```

  - CORS(교차 출처 정책 - Cross-Origin Resource Sharing)
    웹 브라우저는 Same Origin Policy에 따라 웹 페이지와 리소스를 요청하는 곳(ex REST API 서버)이 서로 다른 출처(포트까지 포함)일 때, 서버에서 얻은 결과를 사용할 수 없게 막는다.
      서버에 요청하고 응답을 받아오는 것까지는 이미 진행이 다 된 상황이란 점에 주의!
  
  - REST API 서버에서 Headers에 `Access-Control-Allow-Origin` 속성을 추가하면 된다.

  - CORS 패키지 설치

    ```zsh
      npm i cors
      npm i -D @types/cors

  - CORS 미들웨어 사용(패키지 설치 후)

    ```zsh
      // express-demo-app -> 서버단에 적용
      import express from 'express';
      import cors from 'cors';

      const app = express();

      app.use(cors());
    ```
