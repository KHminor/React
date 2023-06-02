### `Element & Rendering`

- Element

  - 엘리먼트는 React 앱의 가장 작은 단위
  - 엘리먼트는 화면에 표시할 내용을 기술

- DOM에 엘리먼트 렌더링하기

  - HTML 파일 어딘가에 <div> 가 있다고 할 때

    ```jsx
    <div id="root"></div>
    ```

    이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 루트 DOM 노드라고 부른다고 한다.

  - React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM 노드가 있다.

  - React를 기존 앱에 통합하려는 경우 원하는 만큼 수 많은 독립된 루트 DOM 노드가 있을 수 있다.

  - React 엘리먼트를 렌더링 하기 위해서는 우선 DOM 엘리먼트를 ReactDOM.createRoot()에 전달한 다음, React 엘리먼트를 root.render()에 전달해야 한다.

    ```jsx
    const root = ReactDOM.createRoot(
      document.getElementById('root')
    );
    const element = <h1>Hello, world</h1>;
    root.render(element);
    ```

    위와 같이 코드를 작성하면 화면에 Hello, world가 보이게 된다.

- 렌더링 된 엘리먼트 업데이트하기

  - React 엘리먼트는 불변객체이다.

  - 엘리먼트를 생성한 이후에는 해당 엘리먼트의 자식이나 속성을 변경할 수 없다.

  - 엘리먼트는 영화에서 하나의 프레임과 같이 특정 시점의 UI를 보여준다.

  - 지금까지 소개한 내용을 바탕으로 하면 UI를 업데이트하는 유일한 방법은 새로운 엘리먼트를 생성하고 이를 root.render()로 전달하는 것.

    ```jsx
    const root = ReactDOM.createRoot(
      document.getElementById('root')
    );
    
    function tick() {
      const element = (
        <div>
          <h1>Hello, world!</h1>
          <h2>It is {new Date().toLocaleTimeString()}.</h2>
        </div>
      );
      root.render(element);
    }
    
    setInterval(tick, 1000);
    ```

    위와 같이 코드를 작성하면 초 단위로 root.render()를 호출하게 된다.

    물론 실제 대부분의 React 앱은 root.render()를 한 번만 호출한다고 한다.

- 변경된 부분만 업데이트하기

  - React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트한다.