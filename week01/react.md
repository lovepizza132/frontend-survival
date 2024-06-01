# 키워드

## 강의내용

### 리액트 사용

1. 렌더링
- `createRoot` 후 `root.render();` 실행
    ```zsh
    function Greeting() {
        return (
            <p>Hello, world!</p>
        );
        }

        function main() {
        const element = document.getElementById('root');

        if (!element) {
            return;
        }

        const root = ReactDOM.createRoot(element);

        root.render(<Greeting />);
    }

    main();
    ```