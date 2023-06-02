### `Using the Effect Hook`

Effect Hook을 사용하면 함수 컴포넌트에서 side effect를 수행할 수 있다.

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

- useEffect가 하는 일은?

  - React에게 컴포넌트가 렌더링 이후에 어떤 일을 수행해야하는지를 수행.
  - useEffect를 사용하면 React는 우리가 넘긴 함수를 기억했다가 DOM 업데이트를 수행한 이후에 불러낸다.

- useEffect를 컴포넌트 안에서 불러내는 이유는?

  - useEffect를 컴포넌트 내부에 DOM으로써 effect를 통해 count state 변수에 접근할 수 있게 된다.

- useEffect는 렌더링 이후에 매번 수행되는 걸까?

  - 기본적으로 첫번째 렌더링과 이후의 모든 업데이트에서 수행된다.
    - 물론 필요에 맞게 수정하는 방법또한 있다.

- 정리(clean-up)를 이용하는 Effects

  - 메모리 누수가 발생하지 않도록 정리(clean-up)하는 것은 매우 중요하다고 한다.
  - 사용방법
    - Effect 함수가 return(반환) 하게 되면 정리할 수 있게 된다.

- Effect에서 함수를 반환하는 이유는?

  - effect를 위한 추가적인 정리(Clean-up)하기 위한 메커니즘.
  - 모든 effect는 정리를 위한 함수를 반환할 수 있다.

- React가 Effect를 정리하는 시점은 정확히 언제일까?

  - React는 컴포넌트가 마운트 해제되는 떄에 정리를 실행한다.
  - 하지만 Effect는 한번이 아니라 렌더링이 실행되는 때마다 실행된다.

- Effect를 건너뛰어 성능 최적화하기

  - clean-up을 너무 하게 되면 성능이 저하되기 때문에 간단한 경우엔 선택적 인수를 두 번째 인수로 배열을 넘기면 된다.

    ```jsx
    useEffect(() => {
      document.title = `You clicked ${count} times`;
    }, [count]); // count가 바뀔 때만 effect를 재실행합니다.
    ```