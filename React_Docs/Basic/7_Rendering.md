### `조건부 렌더링`

- 조건부 렌더링

  - if 나 조건부 연산자와 같은 JS 연산자를 사용해서 조건에 따라 렌더링가능

    ```jsx
    function Greeting(props) {
      const isLoggedIn = props.isLoggedIn;
      if (isLoggedIn) {
        return <UserGreeting />;
      }
      return <GuestGreeting />;
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root')); 
    // Try changing to isLoggedIn={true}:
    root.render(<Greeting isLoggedIn={false} />);
    ```

    ```jsx
    class LoginControl extends React.Component {
      constructor(props) {
        super(props);
        this.handleLoginClick = this.handleLoginClick.bind(this);
        this.handleLogoutClick = this.handleLogoutClick.bind(this);
        this.state = {isLoggedIn: false};
      }
    
      handleLoginClick() {
        this.setState({isLoggedIn: true});
      }
    
      handleLogoutClick() {
        this.setState({isLoggedIn: false});
      }
    
      render() {
        const isLoggedIn = this.state.isLoggedIn;
        let button;
        if (isLoggedIn) {
          button = <LogoutButton onClick={this.handleLogoutClick} />;
        } else {
          button = <LoginButton onClick={this.handleLoginClick} />;
        }
    
        return (
          <div>
            <Greeting isLoggedIn={isLoggedIn} />
            {button}
          </div>
        );
      }
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root')); 
    root.render(<LoginControl />);
    ```

- 논리 연산자 &&로 if를 인라인으로 표현하기

  - JSX 안에서는 중괄호를 이용해서 표현식을 포함 할 수 있다.

  - 그 안에는 JS의 논리 연산자 &&를 사용하면 쉽게 엘리먼트를 조건부로 넣을 수 있다.

    ```jsx
    function Mailbox(props) {
      const unreadMessages = props.unreadMessages;
      return (
        <div>
          <h1>Hello!</h1>
          {unreadMessages.length > 0 &&
            <h2>
              You have {unreadMessages.length} unread messages.
            </h2>
          }
        </div>
      );
    }
    
    const messages = ['React', 'Re: React', 'Re:Re: React'];
    
    const root = ReactDOM.createRoot(document.getElementById('root')); 
    root.render(<Mailbox unreadMessages={messages} />);
    ```

- 조건부 연산자로 If-Else 구문 인라인으로 표현하기 (삼항 연산자)

  ```jsx
  render() {
    const isLoggedIn = this.state.isLoggedIn;
    return (
      <div>
        The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
      </div>
    );
  }
  
  // 또는 
  
  render() {
    const isLoggedIn = this.state.isLoggedIn;
    return (
      <div>
        {isLoggedIn
          ? <LogoutButton onClick={this.handleLogoutClick} />
          : <LoginButton onClick={this.handleLoginClick} />
        }
      </div>
    );
  }
  ```

- 컴포넌트가 렌더링하는 것을 막기

  - 해당 데이터의 값에 따라 렌더링 될 수도 안될 수도 있도록 하기

    ```jsx
    function WarningBanner(props) {
      if (!props.warn) {
        return null;
      }
    
      return (
        <div className="warning">
          Warning!
        </div>
      );
    }
    
    class Page extends React.Component {
      constructor(props) {
        super(props);
        this.state = {showWarning: true};
        this.handleToggleClick = this.handleToggleClick.bind(this);
      }
    
      handleToggleClick() {
        this.setState(state => ({
          showWarning: !state.showWarning
        }));
      }
    
      render() {
        return (
          <div>
            <WarningBanner warn={this.state.showWarning} />
            <button onClick={this.handleToggleClick}>
              {this.state.showWarning ? 'Hide' : 'Show'}
            </button>
          </div>
        );
      }
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root')); 
    root.render(<Page />);
    ```