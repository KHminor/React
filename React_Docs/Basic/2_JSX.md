### `JSX`

```javascript
const element = <h1>Hello, world!</h1>
```

위의 태그 문법은 JSX라고 하며 JS를 확장한 문법이라고 한다.

JSX는 JS의 모든 기능이 포함되어 있다.

- JSX란?

  - React에서는 본질적으로 렌더링 로직이 UI 로직 (이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식 등)과 연결된다는 사실을 받아들인다.
  - React는 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다 포함하는 ‘컴포넌트’라고 부르는 느슨하게 연결된 유닛으로 관심사를 분리한다.
  - React는 JSX 사용이 필수는 아니지만, 대부분의 사람들은 JS 코드 안에서 UI 관련 작업을 할 때 시각적으로 더 도움이 된다고 생각한다.

- JSX에 표현식 포함하기

  ```jsx
  const name = 'hongmin'
  const element = <h1>Hello, {name}</h1>
  ```

  - JSX의 중괄호 안에는 유효한 모든 JS표현식을 넣을 수 있다.

  ```jsx
  function formatName(user) {
    return user.firstName + ' ' + user.lastName;
  }
  
  const user = {
    firstName: 'Harper',
    lastName: 'Perez'
  };
  
  const element = (
    <h1>
      Hello, {formatName(user)}!
    </h1>
  );
  ```

- JSX도 표현식

  - 컴파일이 끝나면, JSX 표현식이 정규 JS 함수 호출이 되고 JS 객체로 인식된다.

  - 즉, JSX를 if 구문 및 for loop 안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로부터 반환할 수 있다.

    ```jsx
    function getGreeting(user) {
      if (user) {
        return <h1>Hello, {formatName(user)}!</h1>;
      }
      return <h1>Hello, Stranger.</h1>;
    }
    ```

- JSX 속성 정의

  - 문자열 리터럴: 따옴표

    ```jsx
    const element = <a href="<https://www.reactjs.org>"> link </a>;
    ```

  - JS 표현식: 중괄호

    ```jsx
    const element = <img src={user.avatarUrl}></img>;
    ```

  - 따옴표 또는 중괄호 중 하나만 사용하고, 동일한 어트리뷰트에 두 가지를 동시 사용 X

  - JSX는 카멜 케이스로 작성한다고 한다. (JS에 가깝기 때문에)

- JSX로 자식 정의

  - 태그가 비어있다면 XML처럼 /> 를 이용해서 바로 닫아주기

    ```jsx
    const element = <img src={user.avatarUrl} />;
    ```

  - JSX 태그는 자식을 포함할 수 있다.

    ```jsx
    const element = (
      <div>
        <h1>Hello!</h1>
        <h2>Good to see you here.</h2>
      </div>
    );
    ```

- JSX는 주입 공격을 방지합니다.

  - (아래의 코드인 response.potentiallyMaliciousInput 을 사용해야 안전한건가..?)

  ```jsx
  const title = response.potentiallyMaliciousInput;
  // 이것은 안전합니다.
  const element = <h1>{title}</h1>;
  ```

  - 기본적으로 React DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 이스케이프 하므로, 어플리케이션에서 명시적으로 작성되지 않은 내용은 주입되지 않는다.
  - 또한 모든 항목은 렌더링 되기 전에 문자열로 변환된다.
  - 이런 특성으로 XSS 공격을 방지할 수 있다.

- JSX는 객체를 표현한다.

  ```jsx
  const element = (
    <h1 className="greeting">
      Hello, world!
    </h1>
  );
  
  // 위아래 두 예시는 동일하다고 한다.
  
  const element = React.createElement(
    'h1',
    {className: 'greeting'},
    'Hello, world!'
  );
  ```

  - React.createElement()는 버그가 없는 코드를 작성하는데 도움이 되도록 몇 가지 검사를 수행하며, 다음과 같은 객체를 생성한다고 한다.

    ```jsx
    // 주의: 다음 구조는 단순화되었습니다
    const element = {
      type: 'h1',
      props: {
        className: 'greeting',
        children: 'Hello, world!'
      }
    };
    ```

    이러한 객체를 React Element라고 하며, 화면에서 보고 싶은 것을 나타내는 표현이라고 생각하면 된다.