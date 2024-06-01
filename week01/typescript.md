# 키워드

## 강의내용

### 타입스킈립트 사용

1. 타입스크립트 실행
- npx ts-node 
    - 설치가 안되어있어도 사용 가능
    - 근데 나는 안돼서 npm install -g ts-node 후 사용
    - npm list 하면 설치되어있음

2. 타입 지정
- 복잡한 오브젝트의 타입을 재사용하기 위해 타입을 정의할 수 있다.
  ```zsh
  let name: string;
  let age: number;

  name = '홍길동';
  age = 13;

  name = 13; // error TS2322: Type 'number' is not assignable to type 'string'.
  age = '홍길동'; // error TS2322: Type 'string' is not assignable to type 'number'.

  let human: {
    name: string;
    age: number;
  };

  human = { name: '홍길동', age: 13 };
  ```

3. type과 interface
- 확장(상속)하는 법
  - interface는 `extends` 키워드를 이용해 확장
    ```zsh
    interface Person {
      name: string;
      age: number;
    }

    interface Student extends Person {
      school: string;
    }

    const ain: Student = {
      name: 'ain',
      age: '17',
      school: 'high'
    }
    ```
  
  - type은 `&` 기호를 이용해 확장
    ```zsh
    type Person = {
      name: string;
      age: number;
    }

    type Student = Person & {
      school: string;
    }

    const jieun: Student = {
      name: 'jieun',
      age: 27,
      school: 'HY'
    }
    ```
- 선언적 확장(Declaration Merging)
  - interface는 선언적 확장 가능 `같은 이름의 interface 선언 시 자동 확장`
    ```zsh
    interface Person {
      name: string;
      age: number;
    }

    interface Person {
      gender: string;
    }

    const ain: Person = {
      name: 'jieun',
      age: 27,
      gender: 'male'
    }
    ```
  - type은 선언적 확장 불가능(`타입 객체의 확장성 interface < type`)
    ```zsh
    type Person = {
      name: string;
      age: number;
    }

    type Person = { // ❗️Error: Duplicate identifier 'Person'.
      gender: string;
    }
    ```
- 자료형(type)
  - interface는 `Object` 타입만 가능(원시 자료형 불가능)
    ```zsh
    interface name extends string { // ❌ 불가능
      ...
    }
    ```
  - type은 원시값(Primitive type), 튜플(Tuple), 유니언(Union)에 유리
    ```zsh
    type Name = string; // primitive
    type Age = number;
    type Person = [string, number, boolean]; // tuple
    type NumberString = string | number; // union
    type Person = { // 객체는 interface를 사용하도록 하자.
      name: string,
      age: number,
      gender: string
    }
    ```
- computed value 사용
  - interface computed value 사용 불가능
    ```zsh
    type Subjects = 'math' | 'science' | 'sociology';

    interface Grades {
      [key in Subjects]: string; // ❗️Error: A mapped type may not declare properties or methods.
    }
    ```
  - type computed value 사용 가능
    ```zsh
    type Subjects = 'Math' | 'Science' | 'Sociology';

    type Grades = {
      [key in Subjects]: string;
    }
    ```
- 결론
        `type`은 모든 타입 사용 가능 | 확장 '&' | 선언적 확장 X
        `interface`는 객체 타입만 사용 가능 | 확장 'extends' | 선언적 확장 O

3. 타입 추론(Types by Inference)
- 변수를 생성하면서 동시에 특정 값에 할당하는 경우, TypeScript는 그 값을 해당 변수의 타입으로 사용
  ```zsh
  let helloWorld: string = 'Hello World';

  let helloWorld = 'Hello World';
  ```

4. Union Type
- 유니언은 타입이 여러 타입 중 하나일 수 있음을 선언하는 방법
  ```zsh
  type WindowStates = "open" | "closed" | "minimized";
  type LockStates = "locked" | "unlocked";
  type OddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;

  function wrapInArray(obj: string | string[]) {
  if (typeof obj === "string") {
      return [obj];
  //          ^?
    } else {
      return obj;
    }
  }
  ```

5. Optional Parameter
- 함수 매개변수에서 undefined인 경우 '?'를 사용해 Optional Parameter로 처리
  ```zsh
    function greeting({ name, age }: { name: string; age?: number; }): string {
      return age ? `${name} (${age})` : name;
    }
  ```

6. Intersection Type
- 타입 확장하는 간단한 방법
  ```zsh
  type Human = {
    name: string;
    age: number;
  };

  type Creature = {
    hp: number;
    mp: number;
  };

  type Person = Human & Creature;

  let person: Person;

  person = { name: '홍길동', age: 13, hp: 256, mp: 16 };
  ```