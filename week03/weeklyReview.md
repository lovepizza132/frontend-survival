# 3주차 주간회고

자동차를 조립하는 기분이다.
긴 하나의 코드가 함수로, 컴포넌트로 나뉘는게 기분이 아주 좋다.

Inverse Data Flow를 이해하니 React가 아주 즐겁다.

늦었지만 4주차도 빨리 진행해야겠다.

- Parcel encountered errors
Error: Expected content key (error key)  to exist
  - JavaScript에서 다른 패키지를 import 못할 때 발생
  - root directory에서 `parcel-cache`를 삭제하면 된다.

  ```zsh
  rm -r .parcel-cache
  ```
