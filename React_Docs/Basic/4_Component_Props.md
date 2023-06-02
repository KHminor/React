### `Component & Props`

- 함수 컴포넌트와 클래스 컴포넌트

  - 함수 컴포넌트

    ```jsx
    function Welcome(props) {
      return <h1>Hello, {props.name}</h1>;
    }
    ```

  - 클래스 컴포넌트

    ```jsx
    class Welcome extends React.Component {
      render() {
        return <h1>Hello, {this.props.name}</h1>;
      }
    }
    ```

  - class는 몇 가지 추가 기능이 있다고 한다.

- 컴포넌트 렌더링

  - React 엘리먼트는 사용자 정의 컴포넌트로도 나타낼 수 있다.

    ```jsx
    const element = <Welcome name="Sara" />;
    ```

  - React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달한다.

    - 이 객체를 props라고 한다.

    ```jsx
    function Welcome(props) {
      return <h1>Hello, {props.name}</h1>;
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    const element = <Welcome name="Sara" />;
    root.render(element);
    ```

    여기서 <Welcome name={Sara} /> 또한 가능

    또한 주의할 점은 컴포넌트의 첫 글자는 대문자이어야 한다는 것!

- 컴포넌트 추출 (단순화)

  ```jsx
  function Comment(props) {
    return (
      <div className="Comment">
        <div className="UserInfo">
          <img className="Avatar"
            src={props.author.avatarUrl}
            alt={props.author.name}
          />
          <div className="UserInfo-name">
            {props.author.name}
          </div>
        </div>
        <div className="Comment-text">
          {props.text}
        </div>
        <div className="Comment-date">
          {formatDate(props.date)}
        </div>
      </div>
    );
  }
  ```

  - Avatar 를 추출한다면

    ```jsx
    function Avatar(props) {
      return (
        <img className="Avatar"
          src={props.user.avatarUrl}
          alt={props.user.name}
        />
      );
    }
    ```

    ```jsx
    function Comment(props) {
      return (
        <div className="Comment">
          <div className="UserInfo">
            <Avatar user={props.author} />
            <div className="UserInfo-name">
              {props.author.name}
            </div>
          </div>
          <div className="Comment-text">
            {props.text}
          </div>
          <div className="Comment-date">
            {formatDate(props.date)}
          </div>
        </div>
      );
    }
    ```

  - UserInfo를 추출한다면

    ```jsx
    function UserInfo(props) {
      return (
        <div className="UserInfo">
          <Avatar user={props.user} />
          <div className="UserInfo-name">
            {props.user.name}
          </div>
        </div>
      );
    }
    ```

    ```jsx
    function Comment(props) {
      return (
        <div className="Comment">
          <UserInfo user={props.author} />
          <div className="Comment-text">
            {props.text}
          </div>
          <div className="Comment-date">
            {formatDate(props.date)}
          </div>
        </div>
      );
    }
    ```

- props.는 읽기 전용

  - 함수 컴포넌트나 클래스 컴포넌트 모두 컴포넌트의 자체 props를 수정해서는 안된다.

    ```jsx
    function sum(a, b) {
      return a + b;
    }
    ```

    이런 함수를 순수 함수라고 한다.

    (입력값을 변경하지 않고 항상 동일한 입력값에 대해 동일한 결과를 반환하기 때문)

  - 반면 자신의 입력값을 변경하는 것은 순수 함수가 아니다.

    ```jsx
    function withdraw(account, amount) {
      account.total -= amount;
    }
    ```

  - 그래서 모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수로 동작해야 한다.