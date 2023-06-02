### `Hook 개요`

- State Hook

  - 버튼을 클릭하면 값이 증가하는 코드

    ```jsx
    import React, { useState } from 'react';
    
    function Example() {
      // "count"라는 새 상태 변수를 선언합니다
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

    - useState에는 현재의 state값과 state 값을 업데이트 할 수 있는 함수를 쌍으로 정의한다.

  - 여러 state 변수 선언하기

    - 하나의 컴포넌트 내에서 state Hook을 여러 개 사용할 수도 있따.

      ```jsx
      function ExampleWithManyStates() {
        // 상태 변수를 여러 개 선언했습니다!
        const [age, setAge] = useState(42);
        const [fruit, setFruit] = useState('banana');
        const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
        // ...
      }
      ```

  - 여기서 Hook 이란?

    - Hook은 함수 컴포넌트에서 React state와 생명주기 기능(Lifecycle features)을 연동할 수 있게 해주는 함수이다.
    - Hook은 class 안에서는 동작하지 않는다
    - 대신 class 없이 React를 사용할 수 있게 해주는 것.

- Effect Hook

  - React 컴포넌트 안에서 데이터를 가져오거나 구독하고, DOM을 직접 조작하는 작업을 이전에도 했을 텐데

  - 이런 모든 동작을 side effects또는 effects라고 한다.

  - 왜냐하면 다른 컴포넌트에 영향을 줄 수도 있고, 렌더링 과정에서는 구현할 수 없는 작업이기 때문.

  - 예를 들어 React가 DOM을 업데이트한 뒤에 문서의 타이틀을 바꾸는 컴포넌트일 경우엔 아래의 코드처럼 작성

    ```jsx
    import React, { useState, useEffect } from 'react';
    
    function Example() {
      const [count, setCount] = useState(0);
    
      // componentDidMount, componentDidUpdate와 비슷합니다
      useEffect(() => {
        // 브라우저 API를 이용해 문서의 타이틀을 업데이트합니다
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

    - useEffect를 사용하면, React는 DOM을 바꾼 뒤에 effect 함수를 실행한다.
    - Effects는 컴포넌트 안에 선언되어있기 때문에 props와 state에 접근할 수 있다.
    - 기본적으로 React는 매 렌더링 이후에 Effects를 실행한다. 첫 번째 렌더링도 포함해서.

  - 물론 Effect를 해제 할 필요가 있다면 해제하는 함수를 반환해주면 된다.

    ```jsx
    import React, { useState, useEffect } from 'react';
    
    function FriendStatus(props) {
      const [isOnline, setIsOnline] = useState(null);
    
      function handleStatusChange(status) {
        setIsOnline(status.isOnline);
      }
    
      useEffect(() => {
        ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
        return () => {
          ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
        };
      });
    
      if (isOnline === null) {
        return 'Loading...';
      }
      return isOnline ? 'Online' : 'Offline';
    }
    ```

    - 해제하는 함수는
      - return () ⇒ {} 로
      - 중괄호안에 작성해주면 된다.

- Hook 사용 규직

  - Hook은 그냥 JS 함수이지만, 두 가지 규칙을 준수해야 한다.
    1. 최상위에서만 Hook을 호출해야 한다.
       1. 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행하지 X
    2. React 함수 컴포너느 내에서만 Hook을 호출해야 한다.
       1. 일반 JS 함수에서는 Hook을 호출해서는 안 된다.

- 나만의 Hook 만들기

  - 개발하다보면 가끔 상태 관련 로직을 컴포넌트 간에 재사용하고 싶은 경우가 있다.

  - 이 문제를 해결하기 위해선 Custom Hook을 만들어 컴포넌트 트리에 새 컴포넌트를 추가하지 않고도 가능하게 해준다.

  - 예시

    - 친구의 접속 상태를 구독하기 위해서 useState와 useEffect Hook을 사용한 FriendStatus 컴포넌트를 다른 컴포넌트에서도 재사용하고 싶다고 가정한다면

    - 먼저 useFriendStatus라는 custom Hook으로 뽑아내기

      ```jsx
      import React, { useState, useEffect } from 'react';
      
      function useFriendStatus(friendID) {
        const [isOnline, setIsOnline] = useState(null);
      
        function handleStatusChange(status) {
          setIsOnline(status.isOnline);
        }
      
        useEffect(() => {
          ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
          return () => {
            ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
          };
        });
      
        return isOnline;
      }
      ```

      - 해당 Hook은 friendID를 인자로 받아서 친구의 접속 상태를 반환해준다.
      - 이제 이것을 여러 컴포넌트에서 사용할 수 있다.

      ```jsx
      function FriendStatus(props) {
        const isOnline = useFriendStatus(props.friend.id);
      
        if (isOnline === null) {
          return 'Loading...';
        }
        return isOnline ? 'Online' : 'Offline';
      }
      ```

      ```jsx
      function FriendListItem(props) {
        const isOnline = useFriendStatus(props.friend.id);
      
        return (
          <li style={{ color: isOnline ? 'green' : 'black' }}>
            {props.friend.name}
          </li>
        );
      }
      ```

      - 위의 코드처럼 css 또한 삼항연산자로 변경 할 수 있다.