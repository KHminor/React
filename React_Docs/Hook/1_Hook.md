### `Hook 소개`

- Hook 소개

  - Hookr을 이용하여 기존 Class 바탕의 코드를 작성할 필요 없이 상태 값과 여러 React의 능을 사용할 수 있다.

    ```jsx
    import React, { useState } from 'react';
    
    function Example() {
      // "count"라는 새로운 상태 값을 정의합니다.
      const [count, setCount] = useState(0);
    
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