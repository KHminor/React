### `Hello World`

알게 된 점

- React 는

  - JS 라이브러리
  - 컴포넌트와 state를 관리하는 라이브러리이며 현재 state와 이전 state의 차이점을 찾아낸다.
  - 데이터에서 변경된 내용을 바탕으로 화면에 뭘 나타낼지 정하며 해당 내용을 인터페이스(ReactDOM)에게 보낸다고 한다.
  - props, state, context가 변할 때마다 React가 해당 데이터들을 사용하는 컴포넌트를 업데이트하고 컴포넌트가 화면에 새로운 내용을 띄우려는지 확인.
  - 만약 새로운 내용이 있다면, React가 ReactDOM에 전달하여 컴포넌트를 화면에 띄우도록 요청

- ReactDOM 은

  - 웹의 인터페이스이며 실제 HTML 요소를 화면에 불러오는 역할을 한다
  - 브라우저의 일부인 Real DOM을 다루기에 ReactDOM은 유저가 보는 화면에 무슨 내용을 띄울지 정한다.
  - ReactDOM은 차이점을 받고, Real DOM을 조정한다.

- 컴포넌트와 Real DOM의 차이

  - 컴포넌트
    - 컴포넌트는 `props, state, context가 바뀔 때마다 재평가된다.`
    - 이후 React가 컴포넌트 함수를 실행
  - Real DOM
    - React가 `컴포넌트의 이전 state와 현재 state를 비교한 뒤 차이점이 있을 때만` 업데이트된다.
    - 즉, Real DOM은 필요할 때만 가끔 바뀌어 효율 면에서 중요하다
    - 전 state와 현 state를 가상으로 비교하는 것은 메모리에서만 처리할 수 있어서 비용이 저렴하다
    - 다만 Real DOM의 내용을 브라우저에 나타내는 것은 복잡하기에 비용이 더 비싸다
    - 그래서 브라우저에 작은 변화라도 여러 번 일어나면 Real DOM이 너무 많이 사용되어 페이지가 느려질 것이기 때문에 Real DOM은 필요할 때만 가끔 바뀐다.

- 예시

  - 이전 데이터

    ```jsx
    <div>
      <h1>Hi there!</h1>
    </div>
    ```

  - 현재

    ```jsx
    <div>
      <h1>Hi there!</h1>
      <p>This is new!</p>
    </div>
    ```

- 정리

  - React는 두 코드에서 차이점을 확인하고 이를 ReactDOM에 보고
  - ReactDOM은 Real DOM을 업데이트하고 변화된 단락인 p태그 내용만을 삽입
  - DOM 전체를 재렌더링 하지 않는다.