# React-Query

`1224`

실시간 데이터가 중요하다면 React-query

- ajax 성공시/실패시 html 을 보여주려면?
- 몇초마다 자동으로 ajax 요청하려면?
- 실패시 몇로 후 요청을 재시도하려면?
- 다음페이지 내용을 미리 가져오는(prefetch)걸 하려면?

물론 위의 내용들은 지금 배운것으로도 가능할 수 있지만 직접하기 귀찮다면

React-query 라이브러리를 사용하면 쉽게 구현 가능하다고 한다.

물론 React-query가 항상 유용하다고는 못한다고 한다.

- 사용예시는 실시간 SNS, 코인 거래소 처럼 실시간 데이터를 계속해서 보여줘야 할 경우.

설치 방법

```jsx
// Terminal 

// 기존의 설치방법
npm install react-query

// 위에처럼 잘못 설치했을 경우엔 
npm uninstall react-query

// 업데이트된 설치방법
npm install @tanstack/react-query
```

```jsx
// index.js

import { QueryClient, QueryClientProvider, useQuery } from '@tanstack/react-query'

const queryClient = new QueryClient()

root.render(
	// QueryClientProvider 로 감싸주기
  <QueryClientProvider client={queryClient}> 
    <Provider store={store}>
      <React.StrictMode>
        <BrowserRouter>
          <App />
        </BrowserRouter>
      </React.StrictMode>
    </Provider>
  </QueryClientProvider>
);
```

해볼 것은 

- url로 axios 요청해서 서버에서 유저이름 가져와 보여주기를 할 것
    
    ```jsx
    // App.js
    
    // 우선 기본적 셋팅이 보이도록 태그 작성
    <Nav className='ms-auto'>반가워요 Kim</Nav>
    ```
    
    ```jsx
    // App.js
    
    //axios 요청으로 해당 데이터 출력해보기
    axios({
      url: 'https://codingapple1.github.io/userdata.json'
    })
    .then((a)=> {
      console.log(a.data);
    })
    ```
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled.png)
    
- 그런데 위에 처럼 일반적으로 요청하는 것 말고 react-query를 이용해서 ajax요청을 한다면
    - useQuery를 사용할 때 주의 할 점
        1. useQuery([변수],()⇒ {}) 로 변수를 대괄호로 감싸줘야 한다.
        2. axios 요청할 경우 return을 사용해줘야 한다.
        3. 성공시, 실패시에도 return 으로 데이터를 줘야한다.
    
    ```jsx
    // App.js
    
    let result = useQuery(['작명'],()=> {
      return axios({
        url: 'https://codingapple1.github.io/userdata.json'
      })
      .then((a)=> {
        return a.data
      })
    })
    ```
    

그렇다면 useQuery()를 사용할 경우의 장점

1. 성공/실패/로딩중 쉽게 파악가능
    
    ```jsx
    let result = useQuery(['작명'],()=> {
      return axios({
        url: 'https://codingapple1.github.io/userdata.json'
      })
      .then((a)=> {
        return a.data
      })
      .catch((e)=> {
        return e
      })
    })
    
    console.log(result.data);
    console.log(result.isFetching);
    console.log(result.error);
    ```
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%201.png)
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%202.png)
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%203.png)
    
    만약 로딩중일 때 ‘로딩중입니다’를 보여주고 싶다면??
    
    ```jsx
    let result = useQuery(['작명'],()=> {
      return axios({
        url: 'https://codingapple1.github.io/userdata.json'
      })
      .then((a)=> {
        return a.data
      })
      .catch((e)=> {
        return e
      })
    })
    
    function App() {
    	return (
    		<div>
    			{result.isLoading ? '로딩중입니다' : result.data.name}
    		</div>
    	)
    }
    ```
    
    만약 if 를 쉽게 작성하려면 아래와 같이 작성해도 된다.
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%204.png)
    
    useQuery를 사용하지 않는다면 위의 코드를 작성하기까지 state를 하나하나 작성해야 하기에 
     사용할 경우 굉장히 편리하다
    
2. 틈만 나면 자동으로 재요청을 해준다. 
    1. 확인하는 방법은 그냥 코드를 작성 후 창을 여기저기 왔다갔다 하게 되면 
     계속해서 요청을 하는 것을 확인 할 수 있다.
    용어로는 refetch 라고 한다.
    2. 실시간으로 갱신해준다
    
    ```jsx
    let result = useQuery(['작명'],()=> {
      return axios({
        url: 'https://codingapple1.github.io/userdata.json'
      })
      .then((a)=> {
        console.log('요청됨');
        return a.data
      })
      .catch((e)=> {
        return e
      })
    })
    ```
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%205.png)
    
    c. 만약 생긴 되는 주기가 너무 잦다면 staleTime을 셋팅해주기
    
    - 아래와 같이 코드를 작성한다면 2초동안은 갱신을 하지 않도록 한다.
    
    ```jsx
    let result = useQuery(['작명'],()=> {
      return axios({
        url: 'https://codingapple1.github.io/userdata.json'
      })
      .then((a)=> {
        console.log('요청됨');
        return a.data
      })
      .catch((e)=> {
        return e
      })
      
    }, {staleTime: 2000})
    ```
    
    d. 그리고 자동 refetch를 끌 수도 있다고 한다.
    
3. 요청이 실패할 시 retry를 알아서 해준다.
    1. 잘못된 주소로 요청시
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%206.png)
    
4. state 공유를 하지 않아도 된다.
    1. 상위 컴포넌트가 있고 하위 컴포넌트가 있을 때 
     하위 컴포넌트로 데이터를 주려고 할 때는 props를 하게 될 텐데 
    2. 그렇게 하지않고 axios 요청을 두번하게 해서 
     같은 곳으로 요청을 2번 하여 props를 사용하지 않도록 해보았을때
     결과는 효율이 좋지 않아 속도 같은 효율적인 부분에서 좋지 않게 된다.
    3. 그런데 useQuery()를 사용하게 된다면 아래와 같은 사진처럼 
    두번의 axios 요청을 하여 효율이 나빠보이겠지만
    4. react-query는 같은 곳으로의 요청을 여러번 하더라도 한번만 요청을 하게 한다고 한다. 
     
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%207.png)
    
5. ajax 결과 캐싱 기능
    1. 요청에 대한 성공 결과를 5분 동안 기록하게 된다.  
    2. 그래서 예를 들어 12시 10분에 실행되어 성공한 요청이 있을 경우
    3. 12시 13분에 다시 한번 요청을 한다면 react-query에서 12시 10분에 생긴
     결과를 우선적으로 보여주고,
    4. 그 다음 GET요청을 해서 더욱 빠른 느낌을 줄 수 있다.
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%208.png)
    
    ![Untitled](React-Query%205bbaec657165431c8a25fa8fec9b45ea/Untitled%209.png)
    

그리고 redux-toolkit을 설치하게 되면 금방 배운 react-query와 유사한

RTK Query도 자동 설치되어있다고 한다.(물론 react-query가 더욱 문법이 쉽다고 함)