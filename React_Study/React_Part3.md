# React3 (Redux)

`1221`

Redux (장바구니 페이지 만들기)

하나의 Route를 만들텐데 Route 안의 element 요소로

조금 긴 HTML 을 넣기 위해 컴포넌트를 만들어서 넣을 예정

그래서 이번에는 src 폴더 안에 routes 폴더를 생성해 

해당 폴더 안에 Cart.js 라는 파일을 만들어서 불러오려고 한다.

그리고 컴포넌트 파일의 첫 글자는 대문자로 하는것이 일반적이라고 한다.

```jsx
// App.js

// Route 생성
<Route path='/cart' element={}>

</Route>
```

이후 컴포넌트 파일 생성

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled.png)

```jsx
function Cart(props) {
  return (
    <div>
      
    </div>
  )
}
```

우선 장바구니 페이지의 경우 표 형식으로 보여주려 한다.

 

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%201.png)

그래서 테이블 태그를 아래와 같이 작성하게 되면 하나하나 만들어야 해서 

우선은 리액트 부트스트랩을 사용했음

```jsx
import {Table} from 'react-bootstrap';

function Cart(props) {
  return (
    <div>
      <Table>
        <thead>
          <tr>
            <th>#</th>
            <th>상품명</th>
            <th>수량</th>
            <th>변경하기</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1</td>
            <td>안녕</td>
            <td>안녕</td>
            <td>안녕</td>
          </tr>
        </tbody>
      </Table> 
    </div>
  )
}
```

여기서 테이블 태그에 대한 설명

- <tr> 태그: 가로줄 생성
- <th> or <td> 태그: 열 생성

장바구니에 대한 state를 생성하려고 하는데

장바구니에 대한 state를 장바구니 컴포넌트에서만 사용하는 것이 아니기에

App, Detail, Cart에서도 필요할텐데 

그럼 질문!

Q. 어디에 state를 만들어야 모두 사용할 수 있을까??

최상위인 App.js 에서 만들면 된다. 

다만 그렇게 되면 props를 계속 해서 작성해주어야 하기 때문에 번거로워 진다.

그래서 우리는 Redux 를 사용하려고 한다.

Redux 를 사용하게 되면 

- 컴포넌트들이 props 없이 state 공유가 가능하다.
- Redux를 설치하게 되면 하나의 JS 파일 안에 state들을 모두 보관할 수 있다.
    
    ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%202.png)
    
- 모든 컴포넌트들이 해당 JS 파일에 있는 state들을 꺼내서 사용할 수 있다.
    
    ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%203.png)
    
- 팁으로 리액트 구인시 대부분 Redux 를 요구한다고 한다.

Redux 설치하기 전에 준비하기

- package.json 파일 확인
    - react 와 react-dom 이 18.1 버전 이상이어야 구동이 된다.
    
    ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%204.png)
    

Redux 설치하기

```jsx
// terminal

npm i @reduxjs/toolkit react-redux
```

Redux 셋팅하기

- src 폴더 안에 store.js 파일 생성하기
    
    ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%205.png)
    
- store.js 파일 안에 해당 코드 입력해주기
    
    ```jsx
    import { configureStore } from '@reduxjs/toolkit'
    
    export default configureStore({
      reducer: { }
    })
    ```
    
- index.js 로 가서 <Provider store={store}>  입력하기
    - Provider 과 store를 import  해오기
    - Provider태그로 요소를 감싸주기
    - Provider 태그 속성인 store에 import 한 store을 넣어주기
    
    ```jsx
    // index.js
    
    import { Provider } from 'react-redux'
    import store from './store'
    
    root.render(
      <Provider store={store}>
        <React.StrictMode>
          <BrowserRouter>
            <App />
          </BrowserRouter>
        </React.StrictMode>
      </Provider>
    );
    ```
    

Redux store에 state 보관하는 법

- createSlice() 함수를 사용하기
    - useState() 역할과 유사하다고 함
- createSlice() 안에 중괄호 사용하여서 name과 initialState 의 값을 넣어주기
- state 하나를 slice 라고 부른다.
    
    ```jsx
    // store.js
    
    import { configureStore, createSlice } from '@reduxjs/toolkit'
    
    createSlice({
      name: 'state 이름',
      initialState: '값'
    })
    ```
    
    현재 유저의 이름을 보관한다고 했을 경우 
     아래와 같이 createSlice에 저장한 후
    
    ```jsx
    // store.js
    
    import { configureStore, createSlice } from '@reduxjs/toolkit'
    
    createSlice({
      name: 'user',
      initialState: 'kim'
    })
    ```
    

등록하기

- 등록시
    1. createSlice ()를 변수에 담기
    2. configureStore() 안의 reducer 의 값으로 
     작명 : 해당 변수.reducer 을 해주기
     (보통 작명을 해당 변수 이름으로 해주기)
    
    ```jsx
    // store.js
    
    import { configureStore, createSlice } from '@reduxjs/toolkit'
    
    let user = createSlice({
      name: 'user',
      initialState: 'kim'
    })
    
    export default configureStore({
      reducer: { 
        user: user.reducer
      }
    })
    ```
    
    ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%206.png)
    

Redux 로 보관하고 있는 state 사용하기

- useSelector() 사용하기
    - import useSelector 해주기
    - useSelector() 안에 arrow function 을 사용하기
        - useSelector((state)⇒ {return state})
    - useSelector()를 변수에 담아서 사용하기
    
    ```jsx
    // 예시로 Cart.js 에서 사용하기
    
    import { useSelector } from 'react-redux'
    
    function Cart(props) {
    
      let a = useSelector((state)=> { return state })
    
      return ()
    ```
    

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%207.png)

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%208.png)

store에서 여러개의 state를 작성하는 방법

- useState 만드는 것처럼 createSlice () 를 하나의 변수에 담아서 사용하며
 name 은 key, initialState는 value 값으로 담아주고 사용하며
- 꼭 reducer에 등록을 해줘야 사용할 수 있다.

```jsx
import { configureStore, createSlice } from '@reduxjs/toolkit'

let user = createSlice({
  name: 'user',
  initialState: 'kim'
})

let stock = createSlice({
  name: 'stock',
  initialState: [10, 11, 12]
})

export default configureStore({
  reducer: { 
    user: user.reducer,
    stock: stock.reducer
  }
})
```

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%209.png)

참고사항

- useSelector 를 편하게 사용하려면
    - store에서 등록을 한 후 사용하려고 할 때 
     예를 들어 Cart 페이지에서 유저에 대한 데이터를 가져오려고 할 때 
     위에서 배운대로 store 데이터를 불러온다고 한다면 아래와 같이 코드를 작성할 텐데
    
    ```jsx
    import {Table} from 'react-bootstrap';
    import { useSelector } from 'react-redux';
    
    function Cart(props) {
    
      let a = useSelector((state)=> { return state })
      console.log(a.user);  // <--- user 데이터 가지고 오기
      return ()
    ```
    
    ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2010.png)
    
    여기서 arrow function의 return 문에서 state.user 처럼
     원하는 value에 대한 key 값을 입력한다면 더욱 편하게 가지고 올 수 있다.
    
    ```jsx
    import {Table} from 'react-bootstrap';
    import { useSelector } from 'react-redux';
    
    function Cart(props) {
    
      let a = useSelector((state)=> { return state.user })
      console.log(a);  // <--- user 데이터 가지고 오기
      return ()
    ```
    
    ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2011.png)
    
    또한 JS 문법으로서 중괄호랑 return 또한 생략이 가능하기에
     아래와 같이 작성 할 수 있다.
    
    ```jsx
    import {Table} from 'react-bootstrap';
    import { useSelector } from 'react-redux';
    
    function Cart(props) {
    
      let a = useSelector((state)=> state.user)
      console.log(a);  // <--- user 데이터 가지고 오기
      return ()
    ```
    

정리

- 그래서 Redux를 무조건 사용하기 보다 간단한 프로젝트의 경우엔 props 를 사용하는 것이 
 코드가 더욱 간단할 것이며
 규모가 좀 더 큰 경우에서는 Redux를 사용하는 것이 더욱 편리할 것!
- 그리고 모든 state를 Redux store에 넣지 말기

숙제

아래의 데이터를 store에 보관하고

장바구니 페이지에서 데이터 바인딩하기

```jsx
[
{id : 0, name : 'White and Black', count : 2},
{id : 2, name : 'Grey Yordan', count : 1}
]
```

해결 방법

- store.js 에서 해당 데이터를 store에 넣기
    - createSlice()를 해당 변수에 담아서 reducer에 담기
        
        ```jsx
        let cartData = createSlice({
          name: 'cartData',
          initialState: [
            {id : 0, name : 'White and Black', count : 2},
            {id : 2, name : 'Grey Yordan', count : 1}
            ]
        })
        
        export default configureStore({
          reducer: { 
            user: user.reducer,
            stock: stock.reducer,
            cartData: cartData.reducer,
          }
        })
        ```
        
- Cart.js 에서 사용하기 위해 useSelector()을 사용해서 cartData 를 가져와서 변수에 담기
    
    ```jsx
    let cartData = useSelector((state)=> {return state.cartData})
    ```
    
- JS 문법으로 array helper method를 이용해서 반복문 사용
    
    ```jsx
    {
      cartData.map((data, idx)=> {
        let index = idx+1
        return (
          <tbody>
            <tr>
              <td>{index}</td>
              <td>{data.id}</td>
              <td>{data.name}</td>
            </tr>
          </tbody>
        )
      })
    }
    ```
    
    ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2012.png)
    
    ---
    
    `1222`
    
    반복문을 사용할 때 key 속성을 주지 않으면 
     Warning이 뜨기도 하지만 나중에 문제가 생길 수 있기에 해주는 것이 좋다.
    
    ```jsx
    <tbody>
      {
        cartData.map((data, idx)=> {
          let index = idx+1
          return ( 
            <tr key={idx}>
              <td>{index}</td>
              <td>{data.id}</td>
              <td>{data.name}</td>
            </tr>
          )
        })
      }
    </tbody>
    ```
    

Redux에서 Store에 저장한 state를 변경하는 방법

state 를 수정하는 함수를 만들기

- 원할 때 그 함수를 실행해달라고 store.js에 요청

state를 수정해주는 함수 만들기 Step

1. reducers : {} 안에 함수를 작성하기
    1. 함수명은 작명하면 되고 
    2. return 안에 변경할 state 값을 넣어주면 된다.
    3. 기존 state를 가져올 때는 작명한 함수의 () 안의 state에서 가져올 수 있다.
    4. 또한 함수를 여러개 만들고자 할 경우엔 콤마(,) 를 입력하고 계속 함수를 만들면 된다.
    
    ```jsx
    let user = createSlice({
    	name: 'user',
    	initialState: 'kim',
    	reducers: {
    		changeName(state) {
    			return ('john kim')
    		},
    		changeage(){
    			return ('66')
    		}
    	}
    })
    ```
    
2. 위에서 만든 함수를 export 하기
    1. createSlice() 를 담는 변수 밖에서 export 하기
    2. 해당 변수이름.actions 를 하게 되면 state 변경함수들이 남게 된다. 
    3. 그래서 최종적으로는 export let {export 할 함수} = createSlice()를 담는 변수.actions
    
    ```jsx
    // 위의 경우에서는
    
    let user = createSlice({
    	name: 'user',
    	initialState: 'kim',
    	reducers: {
    		changeName(state) {
    			return ('john kim')
    		},
    	}
    })
    
    export let {changeName} = user.actions
    ```
    
3. 만든 함수 import 해서 사용하기
    1. dispatch = store.js로 요청을 보내주는 함수
    2. dispatch를 사용할 때는 
        1. dispatch(export 한 함수())
    
    ```jsx
    // 사용할 위치
    // import {export 한 함수명} from '위치'
    
    import {useDispatch, useSelector} from 'react-reduex
    import {changeName} from '../store'
    
    function Cart() {
    	let dispatch = useDispatch()
    }
    
    // 사용
    dispatch(changeName())
    ```
    

store의 state를 변경하는 방법 한번 더 정리

1. state 변경해주는 함수 만들기
2. 함수 export 해주기
3. dispatch( state 변경함수() )

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2013.png)

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2014.png)

복잡한 이유

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2015.png)

![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2016.png)

Redux- state가 object 또는 array일 경우 변경하는 방법

State

- Object의 경우(
    - 호출
    
    ```jsx
    // store.js
    let user = createSlice({
      name: 'user',
      initialState: { name: 'kim', age: 20},
      reducers: {
        changeName(state) {
          return ('john'+ state)
        }
      }
    })
    
    // Cart.js
    {user.name}의 장바구니
    ```
    
    - 변경
        - name 을 park 로 변경하려면 단순하게 하는 방법
            - 똑같이 하나의 object를 name만 변경해서 넣어주면 된다.
            
            ```jsx
            let user = createSlice({
              name: 'user',
              initialState: { name: 'kim', age: 20},
              reducers: {
                changeName() {
                  return ({ name: 'park', age: 20})
                }
              }
            })
            ```
            
        - 여기서 name 만 변경하는 것이라면
            - return 사용 없이 array 또는 object의 경우 직접 수정해도 state가 변경된다고 한다.
            - 잘 작동하는 이유는?
                - Immer.js 라이브러리의 도움으로 된다고 한다.
            
            ```jsx
            let user = createSlice({
              name: 'user',
              initialState: { name: 'kim', age: 20},
              reducers: {
                changeName(state) {
                  state.name = 'park'
                }
              }
            })
            ```
            
        - 잠시 퀴즈
            - 버튼을 누르면 age가 +1 이 되도록 하는 코드를 작성한다면?
            - 순서
                - store.js 에서 나이를 증가시키도록 하는 state 변경 함수를 작성 후 export 해주기
                    
                    ```jsx
                    upAge(state){
                      state.age = state.age +1
                    }
                    
                    export let {changeName, upAge} = user.actions
                    ```
                    
                - Cart.js에서 import에 등록한 다음 버튼 클릭시 요청할 수 있도록 dispatch 사용
                    
                    ```jsx
                    import { changeName, upAge } from '../store';
                    
                    function Cart() {
                    	<h6>{user.name} 장바구니 ({user.age}살)</h6>
                      <button onClick={()=> {dispatch(upAge())}}>나이 증가 버튼</button>
                    }
                    ```
                    
        - 그래서 그냥 state일 때 보다 object일 때 변경하기가 더욱 쉽기 때문에 
         문자 하나만 필요하더라도 일부러 object 형식으로 저장한다고도 한다.
        - 결론: state가 object 또는 array면 retrun 없이 직접 수정해도 된다.
        
        - 그런데 여기서 만약에 버튼 한번 클릭시 3살, 5살, 10살, 20살 이렇게 올리고 싶을 경우
         계속해서 함수를 작성하기엔 너무 비효율적이기 때문에 
         state 변경 함수에 파라미터를 뚫어서 적용하는 방법을 사용하면 좋다.
            
            ```jsx
            // 파라미터를 사용하지 않을 경우
            
            let user = createSlice({
            	name: 'user',
            	initialState: { name: 'kim', age: 20},
            	reducers: {
            		upAge1(state){
            		  state.age = state.age +3
            		},
            		upAge2(state){
            		  state.age = state.age +5
            		},
            		upAge3(state){
            		  state.age = state.age +10
            		},
            		upAge4(state){
            		  state.age = state.age +20
            		}
            	}
            })
            export let {upAge1,upAge2,upAge3,upAge4} = user.actions
            ```
            
            ```jsx
            // 파라미터를 사용할 경우
            // 파라미터 변수.payload 를 해야 해당 파라미터에 입력한 숫자가 들어오게 된다.
            // payload의 뜻은 택배, 소포라는 의미를 가진다고 한다.
            
            let user = createSlice({
            	name: 'user',
            	initialState: { name: 'kim', age: 20},
            	reducers: {
            		upAge(state, action){
            		  state.age += action.payload
            		}
            	}
            })
            export let {upAge} = user.actions
            ```
            
            그래서 우리가 dispatch()를 통해 해당 함수(upAge)에게 요청을 하는데 
             payload를 통해 해당 upAge() 함수 안의 파라미터 값을 실어서 보냄 
             ex) upAge(100) 이면 payload가 upAge()에게 변경 요청을 보낼 때 
                    100 이라는 화물을 실어서 변경 요청을 보내도록 한다.  
            
            그리고 파라미터 작명을 주로 action이라고 작명을 한다.
            
            actions으로 작명하는 이유는 
            
            - 화물 뿐만 아니라 action에 대한 여러가지 정보들도 담겨져 있기 때문
            
            action이란??
            
            - state 변경함수를 action 이라고 한다.
            
            파일 분할 하기
            
            코드가 길면 알아서 import export 하면 된다
            
            위에서 작성한 user state 를 따로 파일을 만들어 분할 하고 싶을 경우
            
            1. state 데이터를 입력할 파일을 생성
                
                ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2017.png)
                
            2. store.js에서 작성한 state 데이터를 입력
                
                ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2018.png)
                
            3. export 해주기
                
                ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2019.png)
                
            4. store.js 에서 import 해주기
                
                ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2020.png)
                
            5. 기존에 해당 데이터를 사용했던 곳에서 import 했던 경로 변경해주기
                
                ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2021.png)
                
        
        숙제
        
        1. +버튼 누르면 수량이 +1 되는 기능을 넣기
            1. 장바구니 상품마다 고유 id 가 있는데 해당 id에 맞는 제품의 수량이 +1 되도록 하기
        2. 디테일 페이지에서 주문하기 버튼을 누르면 장바구니에 상품을 추가하도록 하기
        
        숙제 해결 방법
        
        1. 첫번째 숙제 해결 순서
            1. 기존에 만들어져 있던 cartData에서 reducers 속성을 통해 state 변경 함수를 생성
                
                ```jsx
                // store.js
                
                let cartData = createSlice({
                  name: 'cartData',
                  initialState: [
                    {id : 0, name : 'White and Black', count : 2},
                    {id : 2, name : 'Grey Yordan', count : 1}
                    ],
                  reducers: {
                    changeCartData(state,action) {}
                	}
                ```
                
            2. state의 타입이 array이기 때문에 array helper method 중 filter를 사용하여 
             파라미터 값으로 선택한 요소의 id 값을 보낸 것과
             cartData 중에 id가 파라미터의 값과 같은 data 를 뽑아내서
             해당 데이터의 count 값을 1증가 하도록 해결
                
                ```jsx
                let cartData = createSlice({
                  name: 'cartData',
                  initialState: [
                    {id : 0, name : 'White and Black', count : 2},
                    {id : 2, name : 'Grey Yordan', count : 1}
                    ],
                  reducers: {
                    changeCartData(state,action) {
                      let data = state.filter((data)=> {
                        return data.id === action.payload 
                      })
                      console.log('24번줄의 데이터는 ',data[0])
                      data[0].count += 1 
                    }
                  }
                })
                
                export let {changeCartData} = cartData.actions
                ```
                
            3. 순서가 좀 애매한데 b 순서를 작성하면서 c를 작성했음
            해당 데이터를 사용할 Cart.js에서 map array helper method를 사용할 때 
            해당 버튼을 클릭시 dispatc(changeData())를 실행하게 하면서 파라미터에는
            클릭한 data의 id값을 넣어주어며 요청.
                
                ```jsx
                <tbody>
                  {  
                    cartData.map((data, idx)=> {
                      let index = idx+1
                      console.log(data)
                      return ( 
                        <tr key={idx}>
                          <td>{index}</td>
                          <td>{data.id}</td>
                          <td>{data.name}</td>
                          <td>{data.count}</td>
                          <td>
                            <button onClick={()=> {
                              dispatch((changeCartData(data.id)))
                            }}>+</button>
                          </td>
                        </tr>
                      )
                    })
                  }
                </tbody>
                ```
                
            4. 다만 계속 해결이 되지 않았던 부분이 그냥 data.count += 1 을 했을 때는 적용이 되지 않았기 때문에 계속 만지작 거리다가 data를 log로 찍어봤을 때 [Proxy]로 
            타입이 array로 되어있기에 혹시나 해서 data[0]으로 했더니 해결이 되었다. 
                
                ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2022.png)
                
        
        2. 첫번째 숙제 해결 순서
        
        우선 데이터가 추가된거는 맞지만 실질적으로 cart 페이지에 데이터가 추가된 것을 
         볼 수는 없었어서 정말로 해결이 된건지는 잘 모르겠다.
        
        - 계속 추가는 됐지만 확인을 할 수 없었던 이유는 새로고침이 되어서 그렇다.
        1.  store.js 에서 addCartData() 를 추가했다.
        2. Detail.js 에서 주문하기 버튼을 클릭하면 해당 data의 데이터들을 모두 파라미터로
         전송하였다.
            
            ```
            <div>
                        <button onClick={()=> {
                          dispatch(addCartData(data))
                        }}>주문하기</button>
                      </div>
            ```
            
            ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2023.png)
            
        3. 이후 push를 통해 해당 데이터를 array 안에 추가하였다.
            
            ```jsx
             addCartData(state,action) {
              console.log(state.length)
              let data ={id:action.payload.id, name:action.payload.title, count:0}
              state.push(data)
              console.log(state.length)  
            }
            ```
            
            기존의 데이터는 이렇게 2개인데 주문하기 버튼을 클릭 후 length는 3개가 된다.
            
            ```jsx
            [{id : 0, name : 'White and Black', count : 2},
            	{id : 2, name : 'Grey Yordan', count : 1}
            ]
            ```
            
            ![Untitled](React3%20(Redux)%20244b03be24fb4c1497d6293b4a7116e6/Untitled%2024.png)
            

---

`1223`

응용문제

1. 이미 장바구니에 해당 상품이 있을 경우 추가하지 않도록 하기
    - find 함수를 사용해서 return 값을 변수에 담아 체크한 다음
     타입이 undefined의 경우엔 alert함수를 사용해서 이미 있다고 알려주고
     아닐 경우엔 alert함수를 사용해서 추가했다고 알려준 다음 추가하기
        
        ```jsx
         addCartData(state,action) {
          let data ={id:action.payload.id, name:action.payload.title, count:0}
          let check = state.find((i)=> {
            return i.id === data.id
          })
          console.log(check);
          if (typeof check !== 'undefined' ) {
            alert('이미 장바구니에 해당 상품이 있습니다.')
          }
          else {
            alert('장바구니에 추가했습니다.')
            state.push(data)
          }
        }
        ```
        
2. 장바구니에서 상품 행에 있는 삭제 버튼을 클릭 시 
 해당 상품 id에 맞는 state를 장바구니에서 제거하기 
    - store.js 에서 state에 있는 object를 제거하도록 하는 함수 만들기
    
    ```jsx
    deleteData(state,action) {      
    
    }
    ```
    
    - Cart.js 에서 해당 deleteDate 함수를 import 해온 다음 
     삭제 버튼을 클릭 시 dispatch(deleteData()) 를 하고 params 값으로 
     해당 data의 id 값을 전송해주기
    
    ```jsx
    import { changeCartData, deleteData } from '../store'
    
    <button onClick={()=> {
      dispatch((deleteData(data.id)))
    }}>제거</button>
    ```
    
    - store.js에서 해당 [data.id](http://data.id) 에 맞는 state data가 아닌 data만 filter() 메서드로 찾아 array로 만들어 반환 한 데이터를 변수에 담아 값을 return 해주기
        - 여기서 주의!!
            - state.어쩌구 하는 데이터는 그냥 state.어쩌구 = 어쩌구 로 변환 가능 하지만
             그냥 state를 변경하는 거라면 return state 변경 변수 라고 작성해줘야 한다.
            - ex) [state.id](http://state.id) = 23 or state[0] = ‘park’
            - ex) state 자체를 변경 하는 것이라면
                - return newarray
                
                 
                
                ```
                deleteData(state,action) {
                      console.log(action.payload);
                      let newarray = state.filter((data)=> {
                        return data.id !== action.payload
                      })
                
                      console.log('array?',newarray);
                      return newarray
                    }
                ```
                

---