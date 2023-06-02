### `Hook의 규칙`

- 최상위에서만 Hook을 호출해야 한다.
  - 반복문, 조건문 혹은 중첩된 함수 내에서 Hook을 호출하지 말기.
    - 그래야 컴포넌트가 렌더링 될 때마다 항상 동일한 순서로 Hook이 호출되는 것을 보장한다.
    - useState와 useEffect가 여러 번 호출되는 중에도 Hook의 상태를 올바르게 유지할 수 있도록 해준다.
- 오직 React 함수 내에서 Hook을 호출해야 한다.
  - React함수가 아닌 일반적인 JS 함수에서 호출하지 말기
- 조번부로 Effect를 실행하기를 원한다면 조건문을 Hook인 Effect 내부에 사용하기

---

### `자신만의 Hook 만들기`

- 그냥 흠… 보고 이해해야 하는 부분이라 정리를 할게 좀 애매..?



---

### `Hook API 참고서`

- useState

  ```jsx
  const [state, setState] = useState(initialState);
  ```

  - 상태 유지 값과 그 값을 갱신하는 함수를 반환

- useEffect

  ```jsx
  useEffect(didUpdate);
  ```

  - useEffect에 전달된 함수는 화면에 렌더링이 완료된 후에 수행하게 될 것.

  - Effect는 종종 컴포넌트가 화면에서 제거 될 때 정리해야 하는 리소스를 만든다.

    - 구독 혹은 타이머, ID 와 같은 것.
    - 아래의 코드는 구독을 생성하는 경우

    ```jsx
    useEffect(() => {
      const subscription = props.source.subscribe();
      return () => {
        // Clean up the subscription
        subscription.unsubscribe();
      };
    });
    ```

    - 정리 함수는 메모리 누수 방지를 위해 UI에서 컴포넌트를 제거하기 전에 수행됩니다.
    - 또한 정리를 하지 않고 여러 번 렌더링이 된다면 다음 Effect가 수행되기 전에 이전 Effect가 실행 되기에 정리를 해줘야 한다.

  - Effect의 타이밍

    - useEffect로 전달된 함수는 지연 이벤트 동안에 레이아웃 배치와 그리기를 완료한 후 발생하게 된다.

  - 조건부 Effect 발생

    - 그냥 사용하게 되면 뭔가 변경될 때마다 실행이 되기 때문에 과도한 작업일 수 있다.

    - 그래서 useEffect에 두 번째 인자에 해당 값이 변경될 시에만 작동하도록 실행

      ```jsx
      useEffect(
        () => {
          const subscription = props.source.subscribe();
          return () => {
            subscription.unsubscribe();
          };
        },
        [props.source],
      );
      ```

- useContext

  ```jsx
  const value = useContext(MyContext);
  ```

  - context 객체(React.createContext에서 반환된 값)을 받아 그 context의 현재 값을 반환.

  - context의 현재 값은 트리 안에서 이 Hook을 호출하는 컴포넌트에 가장 가까이에 있는 <Mycontext.Provider>의 value prop에 의해 결정된다.

  - 컴포넌트에서 가장 가까운 <Mycontext.Provider>가 갱신되면 이 Hook은 Mycontext propvider에게 전달된 가장 최신의 context value를 사용하여 렌더러를 트리거.

  - useContext를 호출한 컴포넌트는 context 값이 변경되면 항상 리렌더링 될 것이다.

  - 컴포넌트를 리렌더링 하는 것에 비용이 많이 된다면, 메모이제이션을 사용하여 최적화할 수 있다.

  - useContext를 Context.Provider와 같이 사용하기

    ```jsx
    const themes = {
      light: {
        foreground: "#000000",
        background: "#eeeeee"
      },
      dark: {
        foreground: "#ffffff",
        background: "#222222"
      }
    };
    
    const ThemeContext = React.createContext(themes.light);
    
    function App() {
      return (
        <ThemeContext.Provider value={themes.dark}>
          <Toolbar />
        </ThemeContext.Provider>
      );
    }
    
    function Toolbar(props) {
      return (
        <div>
          <ThemedButton />
        </div>
      );
    }
    
    function ThemedButton() {
      const theme = useContext(ThemeContext);
      return (
        <button style={{ background: theme.background, color: theme.foreground }}>
          I am styled by theme context!
        </button>
      );
    }
    ```