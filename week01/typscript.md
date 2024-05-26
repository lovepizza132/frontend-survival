# 키워드

## 강의내용

### 타입스킈립트 사용

1. 타입스크립트 실행
- npx ts-node 
    - 설치가 안되어있어도 사용 가능
    - 근데 나는 안돼서 npm install -g ts-node 후 사용
    - npm list 하면 설치되어있음

2. 타입 지정
- '''let name: string;
let age: number;

name = '홍길동';
age = 13;

name = 13; // error TS2322: Type 'number' is not assignable to type 'string'.
age = '홍길동'; // error TS2322: Type 'string' is not assignable to type 'number'.

let human: {
  name: string;
  age: number;
};

human = { name: '홍길동', age: 13 };'''
- ''' type Human = {
    name: string;
    age:number;
}; '''
- ''' 인터페이스 확장하기
interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}

const bear = getBear()
bear.name
bear.honey'''
        
- ''' 교집합을 통하여 타입 확장하기

type Animal = {
  name: string
}

type Bear = Animal & {
  honey: Boolean
}

const bear = getBear();
bear.name;
bear.honey;
        
기존의 인터페이스에 새 필드를 추가하기

interface Window {
  title: string
}

interface Window {
  ts: TypeScriptAPI
}

const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});'''
- let numbers: number[];
numbers = [1, 2, 3];
- let anythings: any[];
anythings = ['hp', 256];
let pair: [string, number];
pair = ['hp', 256];

