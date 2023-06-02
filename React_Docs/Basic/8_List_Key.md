### `List와 Key`

- 여러개의 컴포넌트 렌더링 하기

  ```jsx
  const numbers = [1, 2, 3, 4, 5];
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  ```

- Key

  - React가 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 돕는다.

  - key는 엘리먼트에 안정적인 고유성을 부여하기 위해 배열 내부의 엘리먼트에 지정해야 한다.

    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    const listItems = numbers.map((number) =>
      <li key={number.toString()}>
        {number}
      </li>
    );
    ```

  - 여기서 항목의 순서가 바뀔 수 이쓴 경우 Key에 인덱스를 사용하는 것을 권장하지 않는다고 한다.

  - 또한 리스트 항목에 명시적으로 key를 지정하지 않는다면 React는 기본적으로 인덱스를 key로 사용한다고 한다.

- Key로 컴포넌트 추출하기

  - Key는 주변 배열의 context에서만 의미가 있다고 한다.

  - 예를 들어 ListItem 컴포넌트를 추출 한 경우 ListItem 안에 있는 li 태그가 아니라 배열의 <ListItem/> 엘리먼트가 key를 가져야 한다.

    - 잘못된 Key 사용법

      ```jsx
      function ListItem(props) {
        const value = props.value;
        return (
          // 틀렸습니다! 여기에는 key를 지정할 필요가 없습니다.
          <li key={value.toString()}>
            {value}
          </li>
        );
      }
      
      function NumberList(props) {
        const numbers = props.numbers;
        const listItems = numbers.map((number) =>
          // 틀렸습니다! 여기에 key를 지정해야 합니다.
          <ListItem value={number} />
        );
        return (
          <ul>
            {listItems}
          </ul>
        );
      }
      ```

    - 올바른 Key 사용법

      ```jsx
      function ListItem(props) {
        // 맞습니다! 여기에는 key를 지정할 필요가 없습니다.
        return <li>{props.value}</li>;
      }
      
      function NumberList(props) {
        const numbers = props.numbers;
        const listItems = numbers.map((number) =>
          // 맞습니다! 배열 안에 key를 지정해야 합니다.
          <ListItem key={number.toString()} value={number} />
        );
        return (
          <ul>
            {listItems}
          </ul>
        );
      }
      ```

- Key는 형제 사이에서만 고유한 값이어야 한다.

  - Key는 배열 안에서 형제 사이에서만 고유해야 하고 전체 범위에서는 고유할 필요 X.

  - 두 개의 다른 배열을 만들 때 동일한 key를 사용할 수 있다.

    ```jsx
    function Blog(props) {
      const sidebar = (
        <ul>
          {props.posts.map((post) =>
            <li key={post.id}>
              {post.title}
            </li>
          )}
        </ul>
      );
      const content = props.posts.map((post) =>
        <div key={post.id}>
          <h3>{post.title}</h3>
          <p>{post.content}</p>
        </div>
      );
      return (
        <div>
          {sidebar}
          <hr />
          {content}
        </div>
      );
    }
    
    const posts = [
      {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
      {id: 2, title: 'Installation', content: 'You can install React from npm.'}
    ];
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Blog posts={posts} />);
    ```

- JSX에 map() 포함시키기

  ```jsx
  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      <ListItem key={number.toString()}
                value={number} />
    );
    return (
      <ul>
        {listItems}
      </ul>
    );
  }
  ```

  - 위의 코드를 JSX 식으로 한다면

  ```jsx
  function NumberList(props) {
    const numbers = props.numbers;
    return (
      <ul>
        {numbers.map((number) =>
          <ListItem key={number.toString()}
                    value={number} />
        )}
      </ul>
    );
  }
  ```

- 또한 map()가 너무 중첩된다면 컴포넌트로 추출 하는 것이 좋다고 한다.