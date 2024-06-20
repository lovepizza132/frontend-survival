# useHooks 사용해보자

- 대표적인 Hooks
  - useState -> State Hook -> React의 State
  - useEffect -> Side-effect
  - useContext
  - useRef
  - useLayoutEffect -> useEffect와 조금 다름

- useEffecct
  렌더링 이후 해야할 일, 즉 React의 외부와 관련된 일을 정해줄 수 있다.
  기본적으로 렌더링 때마다 실행되므로, 의존성 배열을 통해 언제 이펙트를 실행할지 지정할 수 있다.
  함수를 리턴함으로써 종료 처리할 수 있다.

    ```zsh
      useEffect(() => {
        const savedTitle = document.title;

        const id = setInterval(() => {
          document.title = `Now: ${new Date().getTime()}`;
        }, 100);

        return () => {
          document.title = savedTitle;
          clearInterval(id);
        };
      });
    ```

- useEffect 처음 한번만 실행하기
  의존성 배열에서 아무것도 지정하지 않을 경우 맨 처음 한번만 실행

    ```zsh
      const [products, setProducts] = useState<Product[]>([]);

      useEffect(() => {
        const fetchProducts = async () => {
          const url = 'http://localhost:3000/products';
          const response = await fetch(url);
          const data = await response.json();
          setProducts(data.products);
        };

        fetchProducts();
      }, []);
    ```

- Effect가 두 번 실행되는 이유
  `<React.StrictMode>`로 컴포넌트 전체를 감쌀 경우 Side Effect를 찾으려고 Effect를 두번씩 실행함

- useRef
  컴포넌트의 생애주기 전체에 걸쳐서 유지되는 객체
    (컴포넌트가 없어질 때까지 동일한 객체가 유지된다.)
  객체 자체가 값은 아니고 값을 참조하기 위한 객체
    (언제든지 값 변경 가능)
  state가 변화하면 해당 및 하위 컴포넌트가 리렌더링되지만,레퍼런스 객체의 현재 값(current)이 바뀌더라도 렌더링에 영향 X
  - 주요 용도
    컴포넌트가 사라질 때까지 동일한 값을 써야하는 경우
      Input의 ID 관리
    특히 useEffect 등과 함께 쓰면서 만나는 비동기 상황에서 현재 값을 제대로 쓰고 싶은 경우
    Closuer -> 변수를 capure, bind를 깜빡하는 문제가 종종 발생

- Custom Hook
  평범하게 Extract Function을 실행하면 된다.
  컴포넌트 - PascalCase / Hook - `use`로 시작하는 camelCase

- Hook 규칙
  Function Component 바로 안쪽 (함수 최상위 레벨)에서 호출해야한다.
  Function Component or Custom Hook에서만 호출

- usehooks-ts
  여러 hook들이 있다. 참고해서 봐보면 도움이 될듯

  ```zsh
    npm i usehooks-ts
  ```

  useFetch, useEffectOnce는 사라짐
  