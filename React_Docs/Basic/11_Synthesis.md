### `합성과 상속`

React는 강력한 합성 모델을 가지고 있으며, 상속 대신 합성을 사용하여 컴포넌트 간에 코드를 재사용하는 것이 좋다.

- 컴포넌트에서 다른 컴포넌트를 담기

  - 아래의 코드와 같이 작성한다면 children prop 를 사용사여 자식의 엘리먼트를 출력에 그대로 전달 할 수 있다.

  - 그래서 이러한 방식으로 다른 컴포넌트에서 JSX를 중첩하여 임의의 자식을 전달 가능하다.

    ```jsx
    function FancyBorder(props) {
      return (
        <div className={'FancyBorder FancyBorder-' + props.color}>
          {props.children}
        </div>
      );
    }
    ```

    ```jsx
    function WelcomeDialog() {
      return (
        <FancyBorder color="blue">
          <h1 className="Dialog-title">
            Welcome
          </h1>
          <p className="Dialog-message">
            Thank you for visiting our spacecraft!
          </p>
        </FancyBorder>
      );
    }
    ```

  - 위와 같이 작성하게 되면 FancyBorder 태그 안에 있는 것들이 FancyBorder 컴포넌트의 children prop으로 전달된다.

  - FancyBorder는 {props.children}을 <div> 안에 렌더링하므로 전달된 엘리먼트들이 최종 출력된다.

  - 물론 흔하지는 않지만 컴포넌트에 여러 개의 구멍을 남겨 prop으로 전달 할 수도 있다.

    ```jsx
    function SplitPane(props) {
      return (
        <div className="SplitPane">
          <div className="SplitPane-left">
            {props.left}
          </div>
          <div className="SplitPane-right">
            {props.right}
          </div>
        </div>
      );
    }
    
    function App() {
      return (
        <SplitPane
          left={
            <Contacts />
          }
          right={
            <Chat />
          } />
      );
    }
    ```

- 특수화

  - 더 구체적인 컴포넌트가 일반적인 컴포넌트를 렌더링하고 props를 통해 내용을 구상한다.

    ```jsx
    function Dialog(props) {
      return (
        <FancyBorder color="blue">
          <h1 className="Dialog-title">
            {props.title}
          </h1>
          <p className="Dialog-message">
            {props.message}
          </p>
        </FancyBorder>
      );
    }
    
    function WelcomeDialog() {
      return (
        <Dialog
          title="Welcome"
          message="Thank you for visiting our spacecraft!" />
      );
    }
    ```

  - 합성은 클래스로 정의된 컴포넌트에서도 동일하게 적용된다고 한다.

    ```jsx
    function Dialog(props) {
      return (
        <FancyBorder color="blue">
          <h1 className="Dialog-title">
            {props.title}
          </h1>
          <p className="Dialog-message">
            {props.message}
          </p>
          {props.children}
        </FancyBorder>
      );
    }
    
    class SignUpDialog extends React.Component {
      constructor(props) {
        super(props);
        this.handleChange = this.handleChange.bind(this);
        this.handleSignUp = this.handleSignUp.bind(this);
        this.state = {login: ''};
      }
    
      render() {
        return (
          <Dialog title="Mars Exploration Program"
                  message="How should we refer to you?">
            <input value={this.state.login}
                   onChange={this.handleChange} />
            <button onClick={this.handleSignUp}>
              Sign Me Up!
            </button>
          </Dialog>
        );
      }
    
      handleChange(e) {
        this.setState({login: e.target.value});
      }
    
      handleSignUp() {
        alert(`Welcome aboard, ${this.state.login}!`);
      }
    }
    ```