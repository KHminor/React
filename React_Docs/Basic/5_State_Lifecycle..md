### `State & Lifecycle`



- 함수에서 클래스로 변환하기

  - 5단계로 함수 컴포넌트를 클래스로 변환할 수 있다.

    1. `React.Component`를 확장하는 동일한 이름의 [ES6 class](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes)를 생성합니다.
    2. `render()`라고 불리는 빈 메서드를 추가합니다.
    3. 함수의 내용을 `render()` 메서드 안으로 옮깁니다.
    4. `render()` 내용 안에 있는 `props`를 `this.props`로 변경합니다.
    5. 남아있는 빈 함수 선언을 삭제합니다.

    ```jsx
    class Clock extends React.Component {
      render() {
        return (
          <div>
            <h1>Hello, world!</h1>
            <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
          </div>);
      }
    }
    ```

- 클래스에 로컬 State 추가하기

  - 3단계로 date를 props에서 state로 이동하기

    1. render() 메서드 안에 있는 this.props.date를 this.state.date로 변경하기

       ```jsx
       class Clock extends React.Component {
         render() {
           return (
             <div>        <h1>Hello, world!</h1>        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>      </div>);
         }
       }
       ```

    2. 초기 this.state를 지정하는 class constructor를 추가

       ```jsx
       class Clock extends React.Component {
         constructor(props) {
           super(props);
           this.state = {date: new Date()};
         }
       
         render() {
           return (
             <div>
               <h1>Hello, world!</h1>
               <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
             </div>
           );
         }
       }
       ```

       클래스 컴포넌트는 항상 props로 기본 constructor를 호출

    3. <Clock /> 컴포넌트에서 date props.를 삭제

       ```jsx
       root.render(<Clock />);
       ```

    - 결과

      ```jsx
      class Clock extends React.Component {
        constructor(props) {
          super(props);
          this.state = {date: new Date()};
        }
      
        render() {
          return (
            <div>
              <h1>Hello, world!</h1>
              <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
            </div>
          );
        }
      }
      
      const root = ReactDOM.createRoot(document.getElementById('root'));
      root.render(<Clock />);
      ```

- 생명주기 메서드를 클래스에 추가하기

  - 많은 컴포넌트가 있는 애플리케이션에서 컴포넌트가 삭제될 때 해당 컴포넌트가 사용 중이던 리소스를 확보하는 것이 중요하다고 한다.

  - Clock 컴포넌트 클래스가 처음 DOM에 렌더링 될 때마다 타이머를 설정하려고 한다.

  - 이것은 React에서 마운팅이라고 한다

  - 또한 DOM에서 삭제될 때마다 타이머를 해제하려고 하는것을 언마운팅이라고 한다.

  - 컴포넌트 클래스에서 특별한 메서드를 선언하여 컴포넌트가 마운트되거나 언마운트 될 때 일부 코드를 작동할 수 있다.

    ```jsx
    class Clock extends React.Component {
      constructor(props) {
        super(props);
        this.state = {date: new Date()};
      }
    
      componentDidMount() {
      }
    
      componentWillUnmount() {
      }
    
      render() {
        return (
          <div>
            <h1>Hello, world!</h1>
            <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
          </div>
        );
      }
    }
    ```

    이러한 메서드들을 생명주기 메서드라고 부른다고 한다.

  - componentDidMount() 메서드는 컴포넌트 출력물이 DOM에 렌더링 된 후에 실행된다.

    - 이 메서드가 타이머를 설정하기에 좋은 장소.

    ```jsx
    componentDidMount() {
        this.timerID = setInterval(
          () => this.tick(),
          1000
        );
      }
    ```

  - componentWillUnmount() 메서드는 언마운트 될 시 작동

- State를 올바르게 사용하기

  - setState()에 대해 알아야할 3가지
    1. 직접 State를 수정하지 말기
    2. State 업데이트는 비동기적일 수도 있다.
    3. State 업데이트는 병합된다.