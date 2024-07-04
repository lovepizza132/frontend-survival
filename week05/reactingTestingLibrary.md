# React Testing Library

- 테스트 코드, 즉 컴포넌트를 사용하는 코드를 작성하면서 해당 컴포넌트의 인터페이스를 점검할 수 있다.

- 시간이 지나면 해당 코드에 대한 지식이 감소해 건드리기 힘들기 때문에, 개발하면서 혹은 빠른시간내 테스트 코드를 작성하는게 중요하다.

1. BDD 스타일의 React Testing Library

  ```zsh
  import React, { useRef } from 'react';

  type TextFieldProps = {
    label: string;
    placeholder: string;
    text: string;
    setText: (value: string) => void;
  };

  export default function TextField({
    label, placeholder, text, setText,
  }: TextFieldProps) {
    const id = useRef(`input-${Math.random()}`);

    const handleChange = (event: React.ChangeEvent<HTMLInputElement>) => {
      const { value } = event.target;
      setText(value);
    };

    return (
      <div>
        <label
          htmlFor={id.current}
        >
          {label}
        </label>
        <input
          id={id.current}
          type='text'
          placeholder={placeholder}
          value={text}
          onChange={handleChange}
        />
      </div>
    );
  }
  ```

2. jest.fn()

- 함수 테스트 가능

  ```zsh
  const setText = jest.fn();
  ```

3. beforeEach()와 mockClear()

- 매 테스트 시작 시 beforeEach()를 통해 함수를 초기화 할 수 있다.

  ```zsh
  beforeEach(() => {
    setText.mockClear();
    // 또는 jest.clearAllMocks();
  });
  ```

4. 작성 방법

- 반복되는 코드를 Extract Function하고, fireEvent 등을 통해 인터랙션만 검증한다.

  ```zsh
  fireEvent.change(screen.getByLabelText('Name'), {
    target: {
      value: 'New Name',
    },
  });

  expect(setText).toBeCalledWith('New Name');
  ```

5. API 테스트

- jest.mock() 활용

  ```zsh
  jest.mock('./hooks/useFetchProducts', () => () => [
    {
      category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
    },
  ]);
  ```
