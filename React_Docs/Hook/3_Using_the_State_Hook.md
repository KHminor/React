### `Using the State Hook`

- Hook과 같은 기능을 하는 클래스 예시

  ```jsx
  class Example extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        count: 0
      };
    }
  
    render() {
      return (
        <div>
          <p>You clicked {this.state.count} times</p>
          <button onClick={() => this.setState({ count: this.state.count + 1 })}>
            Click me
          </button>
        </div>
      );
    }
  }
  ```

  - 굳이?

- Hook과 함수 컴포넌트

  ```jsx
  const Example = (props) => {
    // 여기서 Hook을 사용할 수 있습니다!
    return <div />;
  }
  
  // 또는
  
  function Example(props) {
    // 여기서 Hook을 사용할 수 있습니다!
    return <div />;
  }
  ```

- Hook 이란

  - 특별한 함수이다.
  - 예를 들어 useState는 함수 컴포넌트 안에서 사용할 수 있게 해준다.
  - Hook을 사용하는 시점은
    - 함수 컴포넌트를 사용하던 중 state를 추가하고 싶을 때 사용

- State 변수 선언하기

  - 함수 컴포넌트는 this 를 가질 수 없기 때문에 this.state를 할당하거나 읽을 수 없다.

  - 대신 useState Hook을 직접 컴포넌트에 호출

    ```jsx
    import React, { useState } from 'react';
    
    function Example() {
      // 새로운 state 변수를 선언하고, 이것을 count라 부르겠습니다.
      const [count, setCount] = useState(0);
    ```

- State 가져오기

  - 클래스 컴포넌트는 count를 보여주기 위해 this.state.count를 사용

    ```jsx
    <p>You clicked {this.state.count} times</p>
    ```

  - 함수 컴포넌트는 count를 직접 사용 가능

    ```jsx
    <p>You clicked {count} times</p>
    ```

- State 갱신하기

  - 클래스 컴포넌트는 count를 갱신하기 위해 this.setState()를 호출한다.

    ```jsx
    <button onClick={() => this.setState({ count: this.state.count + 1 })}>
        Click me
      </button>
    ```

  - 반면 함수 컴포넌트는 setCount와 count 변수를 가지고 있으므로 this를 호출 X

    ```jsx
    <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    ```