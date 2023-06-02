### `이벤트 처리하기`

- 이벤트 처리하기

  - React에서는 카멜 케이스를 사용한다

  - HTML

    ```jsx
    <button onclick="activateLasers()">
      Activate Lasers
    </button>
    ```

  - React

    ```jsx
    <button onClick={activateLasers}>
      Activate Lasers
    </button>
    ```

  - 그리고 리액트와의 차이점으로

    - React에서는 `false`를 반환해도 기본 동작을 방지할 수 없다.
    - 반드시 `preventDefault`를 명시적으로 호출해야 한다.
    - 예를 들어, 일반 HTML에서 폼을 제출할 때 가지고 있는 기본 동작을 방지하기 위해 다음과 같은 코드를 작성할 수 있습니다.

    ```javascript
    function Form() {
      function handleSubmit(e) {
        e.preventDefault();
        console.log('You clicked submit.');
      }
    
      return (
        <form onSubmit={handleSubmit}>
          <button type="submit">Submit</button>
        </form>
      );
    }
    ```