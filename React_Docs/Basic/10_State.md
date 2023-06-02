### `State 끌어올리기`

- State 끌어올리기

  - 종종 동일한 데이터에 대한 변경사항을 여러 컴포넌트에 반영해야 할 필요가 있다.

  - 이럴 때는 가장 가까운 고통 조상으로 state를 끌어올리는 것이 좋다.

    - 아래의 함수 컴포넌트는 섭씨온도를 의미하는 celsius prop를 받아 해당 온도가 물이 끓기에 충분한지에 대한 여부를 출력한다.

    ```jsx
    function BoilingVerdict(props) {
      if (props.celsius >= 100) {
        return <p>The water would boil.</p>;
      }
      return <p>The water would not boil.</p>;
    }
    ```

  - 그 다음으로 Calculator 라는 컴포넌트는 온도를 입력할 수 있는 input을 렌더링하고 그 값을 this.state.temperature에 저장한다.

  - 또한 현재 입력값에 대한 BoilingVerdict 컴포넌트를 렌더링한다.

    ```jsx
    class Calculator extends React.Component {
      constructor(props) {
        super(props);
        this.handleChange = this.handleChange.bind(this);
        this.state = {temperature: ''};
      }
    
      handleChange(e) {
        this.setState({temperature: e.target.value});
      }
    
      render() {
        const temperature = this.state.temperature;
        return (
          <fieldset>
            <legend>Enter temperature in Celsius:</legend>
            <input
              value={temperature}
              onChange={this.handleChange} />
            <BoilingVerdict
              celsius={parseFloat(temperature)} />
          </fieldset>
        );
      }
    }
    ```

- 흠… 과정이 너무 길어서 그냥 정리본만 본다면

  - React 애플리케이션 안에서 변경이 일어나는 데이터에 대해선 하나만 두어야 한다.
  - 보통의 경우, state는 렌더링에 그 값을 필요로 하는 컴포넌트에 먼저 추가된다.
  - 그러고 나서 다른 컴포넌트 역시 그 값이 필요하게 되면 그 값을 그들의 가장 가까운 공통 조상으로 끌어올리면 된다.
  - 다른 컴포넌트 간에 존재하는 state를 동기화시키려고 노력하는 대신 하향식 데이터 흐름에 기대는 걸 추천한다고 한다.
  - state를 끌어올리는 작업은 양방향 바인딩 접근 방식보단 더 많은 코드를 유발하지만
  - 버그를 찾고 격리하기 더 쉽게 만든다는 장점이 있다.