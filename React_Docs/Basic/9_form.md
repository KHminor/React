### `폼(Form)`

- 폼

  - HTML form 태그는 form 태그 자체가 내부 상태를 가지기 때문에, React의 다른 DOM 엘리먼트와는 다르게 동작한다고 한다.

  - 예를 들어 HTML의 경우 아래 코드에선 해당 form은 name을 받게 된다.

    ```jsx
     <form>
      <label>
        Name:
        <input type="text" name="name" />
      </label>
      <input type="submit" value="Submit" />
    </form>
    ```

    - 위에서 form태그는 사용자가 form을 제출하면 새로운 페이지로 이동하는 기본 HTML form 동작을 수행한다.
    - React에서 동일한 동작을 원한다면 그대로 사용하면 된다.
    - 다만 대부분의 경우, JS 함수로 form의 제출을 처리하고 사용자가 form에 입력한 데이터에 접근하도록 하는 것이 편리하다.
    - 이를 위한 표준 방식은 제어 컴포넌트라고 불리는 기술을 이용하는 것이라고 한다.

- 제어 컴포넌트

  - HTML에서 `<input>`, `<textarea>`, `<select>`와 같은 폼 엘리먼트는 일반적으로 사용자의 입력을 기반으로 자신의 state를 관리하고 업데이트한다.

  - React에서는 변경할 수 있는 state가 일반적으로 컴포넌트의 state 속성에 유지되며 `[setState()](<https://ko.reactjs.org/docs/react-component.html#setstate>)`에 의해 업데이트된다.

  - React에 의해 값이 제어되는 입력 폼 엘리먼트를 “제어 컴포넌트 (controlled component)“라고 한다.

  - 예를 들어, 이전 예시가 전송될 때 이름을 기록하길 원한다면 폼을 제어 컴포넌트 (controlled component)로 작성할 수 있다.

    ```jsx
    class NameForm extends React.Component {
      constructor(props) {
        super(props);
        this.state = {value: ''};
    
        this.handleChange = this.handleChange.bind(this);
        this.handleSubmit = this.handleSubmit.bind(this);
      }
    
      handleChange(event) {
        this.setState({value: event.target.value});
      }
    
      handleSubmit(event) {
        alert('A name was submitted: ' + this.state.value);
        event.preventDefault();
      }
    
      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              Name:
              <input type="text" value={this.state.value} onChange={this.handleChange} />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    }
    ```

- Textarea 태그

  - HTML 에서 Textarea 엘리먼트는 텍스트를 자식으로 정의한다.

    ```jsx
    <textarea>
      Hello there, this is some text in a text area
    </textarea>
    ```

  - React에서 Textarea는 value 속성을 대신 사용한다.

  - 이렇게하면 Textarea를 사용하는 폼은 한 줄 입력을 사용하는 폼과 비슷하게 작성할 수 있다.

    ```jsx
    class EssayForm extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          value: 'Please write an essay about your favorite DOM element.'
        };
    
        this.handleChange = this.handleChange.bind(this);
        this.handleSubmit = this.handleSubmit.bind(this);
      }
    
      handleChange(event) {
        this.setState({value: event.target.value});
      }
    
      handleSubmit(event) {
        alert('An essay was submitted: ' + this.state.value);
        event.preventDefault();
      }
    
      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              Essay:
              <textarea value={this.state.value} onChange={this.handleChange} />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    }
    ```

- Select 태그

  - HTML 에서 Select 는 드롭 다운 목록을 만든다.

    ```jsx
    <select>
      <option value="grapefruit">Grapefruit</option>
      <option value="lime">Lime</option>
      <option selected value="coconut">Coconut</option>
      <option value="mango">Mango</option>
    </select>
    ```

    - selected 옵션이 있으므로 coconut 옵션이 초기값이 된다.

    - React에서는 selected 속성을 사용하는 대신 **최상단 select태그에 value 속성을 사용**한다.

    - 한 곳에서 업데이트만 하면 되기 때문에 제어 컴포넌트에서 사용하기 더 편하다고 한다.

      ```jsx
      class FlavorForm extends React.Component {
        constructor(props) {
          super(props);
          this.state = {value: 'coconut'};
      
          this.handleChange = this.handleChange.bind(this);
          this.handleSubmit = this.handleSubmit.bind(this);
        }
      
        handleChange(event) {
          this.setState({value: event.target.value});
        }
      
        handleSubmit(event) {
          alert('Your favorite flavor is: ' + this.state.value);
          event.preventDefault();
        }
      
        render() {
          return (
            <form onSubmit={this.handleSubmit}>
              <label>
                Pick your favorite flavor:
                <select value={this.state.value} onChange={this.handleChange}>
                  <option value="grapefruit">Grapefruit</option>
                  <option value="lime">Lime</option>
                  <option value="coconut">Coconut</option>
                  <option value="mango">Mango</option>
                </select>
              </label>
              <input type="submit" value="Submit" />
            </form>
          );
        }
      }
      ```

  - 그래서 전반적으로 input, textarea, select 모두 비슷하게 value 속성을 허용하며 동작한다.

  - 꿀팁!!!

    - select 태그에 multiple 속성을 true한다면 value 속성에 배열을 전달 할 수 있다.

    ```jsx
    <select multiple={true} value={['B', 'C']}>
    ```

- file input 태그

  - HTML에서 <input type=”file”> 는 사용자가 하나 이상의 파일을 자신의 장치 저장소에서 서버로 업로드하거나 File API를 통해 JS로 저작할 수 있다.

    ```jsx
    <input type="file" />
    ```

    - 값이 읽기 전용이기 때문에 React에서는 비제어 컴포넌트이다.

- 제어 컴포넌트의 대안

  - 데이터를 변경할 수 있는 모든 방법에 대해 이벤트 핸들러를 작성하고 React 컴포넌트를 통해 모든 입력 상태를 연결해야 하기 때무에 때로는 제어 컴포넌트를 사용하는게 지루할 수 있다.
  - 특히 기존의 코드베이스를 React로 변경하고자 할 때나 React가 아닌 라이브러리나 React 애플리케이션을 통합하고자 할 때 짜증날 수 있다.
  - 이러한 경우에 입력 폼을 구현하기 위한 대체 기술인 비제어 컴포넌트를 확인 할 수 있다.