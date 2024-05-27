# 개발환경 세팅하는 법
## 3번째 실패... 이번에는 성공해야지

## Node
 - 대부분이 Node.js를 사용한다. 그러니 Node.js로 세팅을 해보자!
 
 - 핵심은 트렌드가 바뀌기 때문에 변화하는 개발환경에서 `전체적인 흐름을 파악하고 유연하게 대처하는 능력을 키우자!`

 - Node.js는 반드시 LTS 버전을 설치하자

 - FNM(Fast Node Manager)이 뭐야?
    Node.js 버전 관리 도구(nvm이 느려서 만듦)\
    cross-platform 지원
      - nvm은 window를 지원하지 않음(nvm-windows를 사용)
      - nvm은 bash script 이기 때문에 window 미지원
    nvm < fnm
      - rust로 만듦
    volta와 같이 프로젝트 진입 시 자동으로 node version 변환 가능
    설치와 구성이 nvm보다 쉬움

- 노드버전은 package.json에서 egines 필드로 node와 pnpm 버전 명시
    ```zsh
    {
        "engines": {
            "node": "14",
            "pnpm": "7"
        },
    }
    ```

### 개발환경 구축

### 1. Node.js 세팅(npm 패키지 준비)
 
 `package.json` 생성

 ```zsh
 npm init
 ```
 (npm init -y 한번에 package.json 생성)
 
 name은 kebab-case, Lisp-case

### 2. `.gitignore` 파일 생성
 
 node_modules를 통째로 커밋하는 것을 방지하기 위해
 
 `.gitignore` 파일 생성
 
 [Node - gitignore](https://www.toptal.com/developers/gitignore/api/node)



- Node.js

## 강의내용

### 개발환경 세팅
Node.js 세팅

1. npm 패키지 준비
- npm init (package.json 생성)
- npm init -y (한번에 package.json 생성)
- name은 kebab-case, Lisp-case
- version은 semantic versioning

2. .gitignore 세팅
- node_modules를 통째로 커밋하는 황당한 일을 방지하기 위해
- .gitignore 파일 생성
-  https://www.toptal.com/developers/gitignore에서 node 검색 후 사용

3. typescript 설정
- npm i -D typescript
    - package.json에 devDependencies에 들어감 개발환경에서만 사용되는 툴
    - (dependencies는 프로그램에서 사용)
    - 과거에는 npm install --save-dev

4. npx tsc --init
- node_modules/.bin/tsc --init 명령어와 같다.
- npx는 node_modules에 해당하는 패키지가 설치되어 있으면 찾아서 실행, 만약 설치되어 있지 않더라도 npm 패키지들을 캐시하는 곳에 다운로드 받아서 설치하지 않아도 사용할 수 있도록 해준다.
- "jsx" : "react-jsx" 설정을 맞춰준다.
    - .tsx 파일을 사용하게 해준다.
    - import React를 하지 않아도 사용할 수 있게 해준다.

5. ESLint 설정(정적 분석기)
- JavaScript, TypeScript 정적분석도구
- 주요 기능
    - 코드스타일 검사: 들여쓰기, 따옴표, 세미클론 등 스타일 규칙 검사
    - 오류 검사 잘못된 변수 사용, 선언되지 않은 변수 등 오류 검출
    - 경고 및 권고사항: 최적화, 가독성 향상 등을 위한 경고와 권고사항 제공
- Rules Severities
    - "off" or "0" : 규칙 해제
    - "warn" or "1" : 규칙을 경고로 설정
    - "error" or "2" : 규칙을 에러로 설정, 테스트, 빌드, PR에서 에러 발생
- 예시
    - ``` {
        "rules" : {
            "indent" : [    // 들여쓰기 규칙
                "error",
                "tab"
            ],
            "linebreak-style": [    // 줄바꿈 스타일 규칙
                "error",
                "windows"
            ],
            "quotes" : [    // 문자열 따옴표 규칙
                "error",
                "double"
            ],
            "semi" : [  // 세미클론 규칙
                "error",
                "always"
            ]
        }
    }```
- npm i -D eslint@8.57.0 eslint-config-xo@0.44.0 eslint-config-xo-typescript@4.0.0 eslint-plugin-react@7.34.1
- npx eslint --init
- env에 jest: true 잡아줄것
- .eslintignore 작성

6. react 설치
- npm i react react-dom
- npm i -D @types/react @types/react-dom

7. 테스팅 도구 설치
- npm i -D jest @types/jest @swc/core @swc/jest jest-environment-jsdom @testing-library/react @testing-library/jest-dom
- jestconfig.js 설정(https://github.com/megaptera-kr/textbook/blob/main/usestore-ts-example/jest.config.js)
- npx eslint . (node_modules > eslint의 모든 파일의 에러 찾기)
    - 에러 발생 C:\megaFrontendStudy\my-app\jest.config.js \ 1:1  error  'module' is not defined  no-undef \ ✖ 1 problem (1 error, 0 warnings) module.export -> export default로 수정
- npx eslint --fix .

8. Parcel 설치
- npm i -D parcel
- package.json scripts 수정

9. index.html 생성
- node는 package.json의 main 사용
- Web Server이기에 "source": "index.html"