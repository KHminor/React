# React

`1128`

- 시작 (Terminal 에 입력)
    - npx create-react-app {{프로젝트명}}
    - cd {{프로젝트 명}}
    - npm start
    
1. 리엑스에서 데이터 바인딩
    - {} 중괄호를 사용하여 바인딩 하기 (className과 같은 거의 모든 곳에서 사용이 가능)

```
import './App.css';
import logofrom './logo.svg'

function App() {
    // let post = "강남 고기 맛집"
function 함수() {
return 100
    }

return (
        <div className="App">
      <div className="black-nav">
        <div>개발 Blog</div>
      </div>
            <h4> {함수()} </h4>
      <img src={logo} alt="" />
    </div>
  );
}

exportdefault App;

```

1. JSX에서 Style 속성을 집어넣을 때
    - Vue, Html에서 Style의 속성을 집어넣을 때처럼 style='font-size: 16px' 와 같이 하는 것이 아닌
    - style={스타일} 로 객체 성격을 나타낼 수 있도록 해야한다.
    
    ```
    <div style={
            {font-size: 16px,
            color: 'blue'
            } }>스타일</div>
    ```
    
    - 다수의 스타일을 집어넣을 경우 , 를 기준으로 작성하면 된다
    - 오른쪽의 value의 값은 항상 문자열로 작성
    - 또한 font-size와 같이 케밥케이스로 작성하는 것을 카멜케이스로 변경하여 작성해야한다. (이유는 js에서 -는 뺄셈이기 때문.)
    
    ```
    <div style={ {color: 'black', fontSize: '16px'} }>스타일 복수 작성</div>
    ```
    
    - 여기서 해당 div들에 대해 계속 이렇게 작성하기 귀찮을 경우 바인딩을 사용하여 작성할 수 있다.
    
    ```
    import './App.css';
    import logofrom './logo.svg'
    
    function App() {
    
    let post= {color: 'blue', fontSize: '30px'}
    
    return (
        <div className="App">
          <div className="black-nav">
            <div style={ post }>
                개발 Blog
            </div>
          </div>
        </div>
      );
    }
    
    exportdefault App;
    
    ```
    
2. 리엑트에서 데이터 관리법
    1. 변수에 넣기
        - `변경이 자주 되지 않는 경우의 데이터의 경우 사용하기`
        - let data = '~~~~~~'
    2. State에 넣기
        - state에 데이터를 저장해놓고 사용하는 이유?
            - `state 안의 데이터가 변경되면 새로고침이 없어도 HTML이 자동으로 재랜더링이 되기 때문이다.`
            - 그래서 부드럽게 새로고침 없이 변경이 된다.
            - useState에서 S 대문자는 필수
        - state는 변수 대신 쓰는 데이터 저장공간
        1. 상단에 import React, { useState } from 'react' 추가
        2. useState(데이터)
            - ex) useState("남자 코트 추천");
            - 이렇게 작성을 하게 되면 [a,b] 이런 두개의 array에 생성이 된다.
            - a에는 남자 코트 추천
            - b에는 남자 코트 추천 state를 정정해주는 함수
            - 그래서 요즘에 작성하는 코드 방식은
                - let [a,b] = useState('남자 코트 추천')
                - ES6 destructuring 문법이다.
                    - 파이썬에서는 익숙한 문법으로 파이썬에서는 a,b = 10,20 으로 사용되는데
                    - 리엑트에서는 let [a,b] = [10,20] 이렇게 사용된다.
                    - 그래서 let [글제목,글제목변경] = useState('남자 코트 추천')
            - 또한 useState()안에는 문자, 숫자, array, object 모두 저장가능하다
                - ex.
                - let [글제목,글제목변경] = useState(['남자 코드 추천', '강남 우동 맛집'])
                
                ```
                import React, { useState }from "react";
                import "./App.css";
                // import logo from "./logo.svg";
                
                function App() {
                let [글제목, 글제목변경]= useState(["남자 코드 추천", "강남 우동 맛집"]);
                let [글제목2, 글제목변경2]= useState("여자 코트 추천");
                
                  // let posts = "연제 고기 맛집";
                return (
                    <div className="App">
                      <div className="black-nav">
                        <div>개발 Blog</div>
                      </div>
                      <div className="list">
                        <h3> {글제목[0]} </h3>
                        <h3> {글제목[1]} </h3>
                        <p>11월 28일 발행</p>
                        <hr />
                      </div>
                      <div className="list">
                        <h3> {글제목2} </h3>
                        <p>11월 28일 발행</p>
                        <hr />
                      </div>
                    </div>
                  );
                }
                
                exportdefault App;
                
                ```
                

---

Tip!!

- 태그에 class 를 주고 싶으면? ⇒ div className=”클래스명”
- React, Vue, Angular를 사용하는 이유 데이터 바인딩을 할 수 있기 때문
    - 사용방법
        - 중괄호 안에 해당 변수명을 넣어준다.
        
        ```jsx
        function App() {
        	let post = "강남 고기 맛집"
          return (
        	    <div className="App">
              <div className="black-nav">
                <div>개발 Blog</div>
              </div>
        			<h4> {post} </h4>
            </div>
          );
        }
        ```
        
        또는
        
        ```jsx
        function App() {
        	let post = "강남 고기 맛집"
        	function 함수() {
        		return 100
        	}
         
          return (
        	    <div className="App">
              <div className="black-nav">
                <div>개발 Blog</div>
              </div>
        			<h4> {함수()} </h4>
            </div>
          );
        }
        ```
        
    

---

### 깨알 CSS

- font-weight: 폰트 굵기

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled.png)

---

`1129`

## React

만약 터미널에 뜨는 warning eslint가 보기 싫다면 상단에 주석으로

/* eslint-disable */ 을 작성하면 된다.

그리고 react에서의 addEventListener 

- 옛날 자바 스크립트 방법: onClick=””
- 리엑트: onClick={ 클릭될 때 실행할 함수() }
    - 만약 함수를 작성하기 귀찮다면
    - onClick={ ()⇒{실행할 내용 } } 이렇게 작성할 수도 있다. arrow function
    

클릭시 1증가하도록 만드는 방법

- state를 통해 변수를 생성 후
- state를 생성시 함께 생성했던 함수를 사용하기
    - ex) let [num, numchange] = useState(0) 의 경우
    - num을 0이 아닌 1로 변경하고 싶을 경우
    - numchange(1)을 하게 되면 변경된다.
- 정리
  
    ```jsx
    import React, { useState } from "react"
    
    let [따봉, 따봉변경] = useState(0)
    
    <div onClick={()=> {따봉변경(따봉+1)}}>
    	{따봉} 👍
    </div>
    ```
    
    위와 같이 state를 이용하여 변경해야 재렌더링이 가능하다.
    
- 만약 버튼을 클릭시 남자코트에서 여자코트로 명칭을 변경하려면
    - 기존의 state 데이터를 변경해야하는데 일반적으로 state데이터를 직접적으로
      
        변경하지 않도록 하기 때문에 deepCopy를 해야한다.
        
        - let [성별, 성별변경] = useState([’남자’,’여자’])
        - let newArray = […성별]
        - newArray[0] = 성별[1]
        - 성별변경(newArray)
- 만약 버튼을 클릭시 글제목을 변경시키려 한다면?

```jsx
<button
            onClick={() => {
              let newArray = [...글제목];
              newArray[0] = 글제목[2];
              newArray[1] = 글제목[0];
              newArray[2] = 글제목[1];
              글제목함수(newArray);
            }}
          >
            🐱‍🏍
          </button>
```

---

`1130`

## 리엑트

하나의 return () 소괄호 안에는 하나의 태그만 있어야 한다

HTML을 줄여서 쓸 수 있는 방법:

- 리엑트의 Component 문법
    - (똑같은 태그를 중복해서 작성할 경우 사용)
    - Component 유의사항
        - 함수명의 첫글자는 대문자로 작성
        - return()안에 있는건 태그 하나로 묶어야함
        - 또한 return() 내부를 묶을 때 의미없는 div를 쓰기 싫다면
            - <> </> 이렇게만 작성해도 된다,

```jsx
ex) 아래와 같은 코드를 계속해서 작성하려할 경우
<div className="modal">
  <h2>제목</h2>
  <p>날짜</p>
  <p>상세내용</p>
</div>

기존에 작성된 return() 이 끝나고 난 뒤에 이렇게 작성을 한 후

function {함수명} {
	<div className="modal">
	  <h2>제목</h2>
	  <p>날짜</p>
	  <p>상세내용</p>
	</div>
}

초기에 적혀있었던 return() 안에 
<함수명></함수명> 작성을 하면 적용 할 수 있고
<함수명 /> 이렇게만 작성해도 적용 가능하다.

```

- 어떤걸 Component로 만드는게 좋을까?
    - 반복출연하는 HTML 덩어리들
    - 자주 변경되는 HTML UI들
- Component를 많 이 만들었을 때 단점?
    - state 쓸 때 복잡해진다.
        - 상위 component에서 만든 state를 쓰려면 
         props 문법을 이용해야한다.
    

---

`1201` 유료 결제 시작!!

### [동적인 UI 만드는 step]

1. html CSS로 미리 디자인 완성
   
    ```jsx
    function Modal(){
    	return (
    		<div className="modal">
          <h2>제목</h2>
          <p>날짜</p>
          <p>상세내용</p>
        </div>
    	)
    }
    ```
    
2. UI의 현재 상태를 state로 저장
   
    ```jsx
    // model을 변경할 때 사용하는 setState를 작성할 때는 
    //    set을 붙여주는 것이 관습
    // 현재 상태는 열림/닫힘 or 1/0 or true/false 이렇게 해주면 일반적 
    let [modal, setState] = useState({현재 상태})
    ```
    
3. state에 따라 UI가 어떻게 보일지 작성 
    1. JS라면 {} 중괄호 안에 if문을 사용하거나 하면 되지만
     html이기 때문에 삼항 연산자를 사용하여 조건문을 작성하기.
    
     
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%201.png)
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%202.png)
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%203.png)
    
    그래서 아래의 사진과 같이 작성
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%204.png)
    
    정리하자면 state는 스위치이고 삼항 연산자는 기계라고 생각하면 된다. 
    
    이제 해당 제목을 누르면 모달창을 띄우도록 하려면??
    
    ```jsx
    // 기존의 modal의 값은 false 이기에 바로 modal의 값을 true 바꾸려고 하면 안된다
    // 그래서 state의 값을 변경해주기 위해서 setModal을 사용하여 modal의 값을 변경해줘야한다.
    <div>
    	<h2 onclick={ () => {setModal(true)} }>제목입니다</h2>
    </div>
    
    ```
    
    과제:  제목을 한번 더 누르면 모달창이 사라지도록 하려면??
    
    ```jsx
    // 기존의 코드에서 모달을 변경 할 때 조건만 넣어주면 된다.
    <div>
    	<h2 onclick={ () => {
    		modal == false ? setModal(true) : setModal(false) 
    	}	
    }>제목입니다</h2>
    </div>
    ```
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%205.png)
    
    ### [반복문으로 같은 HTML을 반복 생성하는 법]
    
    우선 array helper methods 로 map을 설명해주셨음
    
    1. array 자료 갯수만큼 함수안의 코드를 실행해준다.
    2. 함수의 파라미터는 array안에 있던 자료
    3. retrun에 뭘 적어주면 해당 데이터를 array로 담아준다.
    
    ```jsx
    [1,2,3].map(function(a) {
    	console.log(a)
    )
    // 1
    // 2
    // 3
    
    [1,2,3].map(function(a) {
    	return a*2
    )
    
    // [2,4,6]
    ```
    
    그래서 html 안에서 반복문을 넣을 수 있는 방법으로는 중괄호 안에 for문을 사용하는건데 
    
    if문과 똑같이 {} 중괄호 안에는 for문을 사용할 수 없기 때문에 
    
    map 메서드를 사용해준다.
    
    ```jsx
    [1,2,3].map(function(){
    	return <div>안녕</div>
    )
    ```
    
     리엑트에서는 array안에 HTML을 담아놔도 잘 보여준다.
    
    그래서 위의 코드를 작성하게 되면 
    
    [<div>안녕</div>,<div>안녕</div>,<div>안녕</div>] 이렇게 작성이 되는데 
    
    리엑트를 거치게 되면 아래와 같이 안녕을 감싸는 div태그가 3개 생성이 된다.
    
    그래서 만약에 태그가 2줄 3줄 이렇게 넘어가게 된다면 소괄호 () 로 return 값을 감싸주면 된다.
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%206.png)
    
    위의 코드를 가지고 이제 글 제목에 적힌 개수만큼 반복해서 글을 보여주려면 아래와 같이 해주면 된다.
    
    ```jsx
    {
    	글제목.map(function(){
    		return (
    			<div>
            <h1>{글제목[1]}</h1>
            {글제목2[1]}
          </div>
    		)
    	})
    }
    ```
    
    다만 위의 코드처럼 작성하게 되면 같은 글만 반복해서 보이기 때문에 
    
    ```jsx
    // 아래처럼 작성하게 되면 article에 있는 데이터를 받아서 출력하게 되며
    {
    	글제목.map(function(article){
    		return (
    			<div>
            <h1>{article}</h1>
            <hr />
          </div>
    		)
    	})
    } 
    
    // 여기서 파라미터으로 article 다음에 하나 더 넣게 되면
    // 반복문을 돌 떄 마다 0부터 1씩 증가하는 정수를 받을 수 있게 된다. 
    // 그래서 사전에 정의했던 글제목2인 날짜를 함께 출력하게 되면
    // 아래와 같이 할 수 있다.
    {
            글제목.map(function(article,i){
              return (
                <div>
                  <h1>{article}</h1>
                  <p>생성 날짜: {글제목2[i]}</p>
                  <hr />
                </div>
              )
            })
          }
    ```
    
    그래서 정리하자면 
    
    map() 함수는
    
    1. 왼쪽 array 자료만큼 내부코드를 실행
    2. return 오른쪽에 있는걸 array로 담아준다.
    3. 유용한 파라미터 2개 사용가능
    
    그래서 비슷한 HTML을 반복하여 생성하려면 map()을 쓰면 된다.
    
    과제 따봉 갯수를 개별로 기록하기
    
    여기서 에러 표시는 key의 고유값을 정해주지 않았기 때문이기에 
    
    - key=”html 마다 다른 숫자” 를 넣어주면 된다.
    
    ```jsx
    //우선 똑디 기억하자!!
    // state에 정의했던 array의 값을 변경할 경우 해당 array를 새로운 변수에 deep copy를 한 후
    // 변경해야만 해당 값에 접근하여 변경할 수 있따.
    // 또한 onclick={안에는 함수를 작성해야하기에 }
    // onclick={()=> {}} <== 이렇게 작성해야 한다는 점.
    
    {
      글제목.map((article,i)=> {
        return (
          <div>
            <h1>{글제목[i]} <span onClick={()=> {
              let up = [...따봉]
              up[i] += 1
              따봉변경(up)
            }}>👍</span> {따봉[i]}</h1>
            {글제목2[i]}
          </div>
        )
      })
    }
    ```
    
    ---
    
    `1203`
    
    리엑트도 다른 언어들과 마찬가지로 함수 안에서 작성한 모든 변수는 
    
    함수 밖에서는 사용할 수가 없다.
    
    현재 App 구조를 본다면 아래의 사진과 같다.
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%207.png)
    
    그래서 App이 부모, Modal이 자식이 된다.
    
    따라서 부모가 가지고 있는 state는 props를 이용해서 자식이 사용할 수 있게 된다.
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%208.png)
    

부모 → 자식 state 데이터를 전송하는 방법

1. <자식 컴포넌트 작명={state이름}>
2. props 파라미터 등록 후 props 작명 사용

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%209.png)

정리

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2010.png)

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2011.png)

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2012.png)

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2013.png)

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2014.png)

그런데 컴포넌트가 많아지면 props가 귀찮아진다.

Q.만약 다양한 색의 모달창이 필요할 경우

1. 자식 컴포넌트에 변수값을 지정하여 해당 색상을 넣어준다.
2. 모달의 style을 지정하는데 여기서 
    - style={} 이렇게 중괄호 하여 적용을 할텐데 해당
    - 해당 중괄호 안에 css를 작성해야 적용할 수 있다.
    - ex. {background-color:props.bgc}
    - 여기서 그냥 문자 자체도 props를 이용하여 전달이 가능하다.
        - modal == true ? <Modal st=’blue’ bgc={'yellow'} 글제목={글제목} /> : null

```jsx
function App() {
	<div>
		{
			modal == true ? <Modal color="skyblue" bgc={'yellow'} 글제목={글제목}  /> : null
		}
	</div>
}
	
function Modal(props) {
  return (
    <div className="modal" style={{backgroundColor:props.color}}>
      <h2>{props.글제목[0]}</h2>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  );
}
```

숙제:

글 수정 버튼을 누르면 첫 글제목이 ‘여자코트 추천’으로 바뀌어야 함

내가 한 해결 방법

1. Modal 컴포넌트에게 props로 글수정버튼이라는 변수에
해당 함수에서 작성한 state의 글제목[1]을 담아서 보내주었고
2. Modal 컴포넌트에서 해당 글수정 버튼을 클릭할 경우 
해당 title이 변경 되도로 하기 위해서 JS를  이용하여 h2 태그 안의 텍스트가 변경되도록 했으며
3. 변경될 타이틀의 값으로는 props로 받아온 글수정버튼을 이용하여 적용
- 여기서 헷갈렸던 부분
    - 리엑트에서 태그 안에 css를 적용할 때 css의 값으로는 문자열로 전달해야 적용된다.
    - innerText값을 넣어줄 때 props를 적용할 때 무조건 중괄호 안에 넣어줘야 하는 줄 알았는데  
     그렇지 않았다는 부분 체크하기
        - 함수의 return 부분으로 넣어줘서 그런지 그냥 props.글수정버튼 이렇게만 해줘도 넣어졌다.

```jsx
import React, { useState } from "react";
import "./App.css";

function App() {
  let [글제목, 글제목함수] = useState(["남자코트", "여자코트", "바지"]);
  let [글제목2, 글제목함수2] = useState(["221127", "221128", "221129"]);
  let [따봉, 따봉변경] = useState([0,0,0]);
  
  let [성별, 성별변경] = useState(["여자", "남자"]);
  let [modal, setModal] = useState(false)

  function 제목바꾸기() {
    let newArray = [...성별];
    newArray[0] = 성별[1];
    성별변경(newArray);
  }

  return (
    <div className="App">
      <div className="black-nav">개발 Blog</div>

      {
        글제목.map((article,i)=> {
          return (
            <div>
              <h1 onClick={()=> {setModal(true)}}>{article} <span style={{cursor: 'pointer'}} onClick={()=> {
                let thumb = [...따봉]
                thumb[i] = 따봉[i] +1
                따봉변경(thumb)
              }}>👍</span>{따봉[i]}</h1>
              <div>{글제목2[i]}</div>
            </div>
          )
        })
      }

      {
        modal == true ? <Modal 글수정버튼={글제목[1]} color="skyblue" bgc={'yellow'} 글제목={글제목}  /> : null
      }

    </div>
  );
}

function Modal(props) {
  return (
    <div className="modal" style={{backgroundColor:props.color}}>
      <h2 id="title">{props.글제목[0]}</h2>
      <p>날짜</p>
      <p>상세내용</p>
      <button onClick={()=> {
        document.getElementById('title').innerText = props.글수정버튼
      }}>글수정</button>
    </div>
  );
}

export default App;
```

강의 선생님이 의도한 것은 다른 방법이어따…

```jsx
글수정버튼이라는 변수에 해당 글제목 state를 변경할 수 있도록 하는 글제목함수를 
 props로 전달하여 onclick시 해당 글제목함수를 실행시켜 기존의 글제목을 변경하도록 작업

import React, { useState } from "react";
import "./App.css";

function App() {
  let [글제목, 글제목함수] = useState(["남자코트", "남자아우터", "바지"]);
  let [글제목2, 글제목함수2] = useState(["221127", "221128", "221129"]);
  let [따봉, 따봉변경] = useState([0,0,0]);
  
  let [성별, 성별변경] = useState(["여자", "남자"]);
  let [modal, setModal] = useState(false)

  function 제목바꾸기() {
    let newArray = [...성별];
    newArray[0] = 성별[1];
    성별변경(newArray);
  }

  return (
    <div className="App">
      <div className="black-nav">개발 Blog</div>

      {
        글제목.map((article,i)=> {
          return (
            <div>
              <h1 onClick={()=> {setModal(true)}}>{article} <span style={{cursor: 'pointer'}} onClick={()=> {
                let thumb = [...따봉]
                thumb[i] = 따봉[i] +1
                따봉변경(thumb)
              }}>👍</span>{따봉[i]}</h1>
              <div>{글제목2[i]}</div>
            </div>
          )
        })
      }

      {
        modal == true ? <Modal 글수정버튼={글제목함수} color="skyblue" bgc={'yellow'} 글제목={글제목}  /> : null
      }

    </div>
  );
}

function Modal(props) {
  return (
    <div className="modal" style={{backgroundColor:props.color}}>
      <h2 id="title">{props.글제목[0]}</h2>
      <p>날짜</p>
      <p>상세내용</p>

      <button onClick={()=> {
        props.글수정버튼(["여자코트", "여자아우터", "바지"])
      }}>글수정</button>
    </div>
  );
}

export default App;
```

Q. 지금 누른 글 제목이 모달창안에 뜨게 하려면?

내가 한 방식

- 우선 state를 하나 따로 정의해서 선택한 글을 담을 변수를 만들고 
 해당 글을 변경시 사용할 함수 또한 정의했다.

```jsx
let [선택글제목,선택글제목변경] = useState(null)
```

- 이후 글 제목을 map으로 돌아가며 반환 할 때 기존에 정의했던 h1 태그를 클릭시 실행되는 
 함수 내부에서 해당 article을 title이라는 변수에 담아준 뒤 
  선택글제목변경함수를 통해 해당 title를 담아주어 선택한 article인 제목을 선택글내용으로 
  변경해주고

```jsx
let title = article
선택글제목변경(title)
```

- props를 통해 전달 후

```jsx
{
  modal == true ? <Modal 선택글제목={선택글제목} 글수정버튼={글제목함수} 
	color="skyblue" bgc={'yellow'} 글제목={글제목}  /> : null
}
```

- 자식 컴포넌트에서 적용해주기

```jsx
function Modal(props) {
  return (
    <div className="modal" style={{backgroundColor:props.color}}>
      <h2 id="title">{props.선택글제목}</h2>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  );
}
```

강사님이 하는 방식

내가 작성한것과 비슷하지만 map() 함수의 두번째 인자로 받아주는 값이 
 인덱스 값으로 0,1,2….. 이렇게 되는 것을 이용해서 0이면 글제목의 인덱스에 접근하도록 하기

```jsx
let [선택글제목,선택글제목변경] = useState(null)

{
  글제목.map((article,i)=> {
    return (
      <div>
        <h1 onClick={()=> {
          선택글제목변경(i)
          setModal(true)
        }}>{article} <span style={{cursor: 'pointer'}} onClick={()=> {
          let thumb = [...따봉]
          thumb[i] = 따봉[i] +1
          따봉변경(thumb)
        }}>👍</span>{따봉[i]}</h1>
        <div>{글제목2[i]}</div>
      </div>
    )
  })
}
```

---

`1205`

리엑트에서 태그는 항상 여는 태그 닫는태그로 있어야한다.

원래 input태그의 경우 여는 태그만 있어도 됐지만 리엑트에서는 닫는 태그도 있어야한다.

만약 하나만 하고 싶다면 

<input></input> 에서 ⇒ <input /> 이거로 변경하면 된다.

input태그 종류

- type=”range”

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2015.png)

- type=”checkbox”

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2016.png)

- type=”date”
  
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2017.png)
    

만약 input태그에 뭔가 입력시 코드를 실행하고 싶다면 

onChange/ onInput 을 작성하면 된다. 

그래서 이벤트핸들러(onClick, onChange, onInput …) 종류는 굉장히 많다.

여기서 input태그 내부의 입력값을 가져오고 싶을 경우 함수의 파라미터값을 가져와서 사용

```jsx
// onchange가 감지할 때마다 생성되는 e
<input onchange={(e)=> { console.log(e) }}/>

// onchange가 감지할 때마다 생성되는 이벤트가 발생한 html태그
<input onchange={(e)=> { console.log(e.tartget) }}/>

// onchange가 감지할 때마다 생성되는 이벤트가 발생한 html태그에 입력한 값
<input onchange={(e)=> { console.log(e.target.value) }}/>
```

그리고 현재 강의대로 작성했다면 아래의 코드가 작성이 되어있을텐데

그렇다면 span 태그에 있는 따봉을 눌러도 모달창이 뜨게된다.

이유는 클릭 이벤트는 상위 html로 퍼지게 되는데 이걸 **이벤트 버블링**이라고 부른다.

```jsx
{
  글제목.map((article,i)=> {
    return (
      <div>
        <h1 onClick={()=> {
          let title = article
          선택글제목변경(title)
          setModal(true)
        }}>{article} <span style={{cursor: 'pointer'}} onClick={()=> {
          let thumb = [...따봉]
          thumb[i] = 따봉[i] +1
          따봉변경(thumb)
        }}>👍</span>{따봉[i]}</h1>
        <div>{글제목2[i]}</div>
      </div>
    )
  })
}
```

그래서 이벤트 버블링 현상을 막고 싶다면 
하위태그에서 클릭 이벤트시 stopPropagation을 넣어주기.

```jsx
{
  글제목.map((article,i)=> {
    return (
      <div>
        <h1 onClick={()=> {
          let title = article
          선택글제목변경(title)
          setModal(true)
        }}>{article} <span style={{cursor: 'pointer'}} onClick={(e)=> {
          e.stopPropagation()
					let thumb = [...따봉]
          thumb[i] = 따봉[i] +1
          따봉변경(thumb)
        }}>👍</span>{따봉[i]}</h1>
        <div>{글제목2[i]}</div>
      </div>
    )
  })
}
```

그런데 console.loe()로 확인을 해보게 되면 늦게 처리된다.

이유는 state변경함수는 늦게처리되는데 이것을 비동기처리라고 한다.

그래서 빠르게 처리될 수 있는 console.log()부터 처리한 뒤 state변경 함수를 처리하게 되서어 
늦게 변경된다.

숙제.

1. 버튼을 누르면 글 하나 추가되는 기능 만들기
    1. 우선 내가한 방식은 강사님이 말씀해주신것처럼 기존에 정의해둔 
     글제목 state를 변수에 담아줌과 동시에 가장 앞에 
         e.target.value를 추가하여 담아주고 
         state 변경하기 위한 함수로 글제목함수에 해당 변수를 넣어주어 해결
        1. 추가> 강사님이 하는 방법은 
            1. title.unshift(입력값) 로 unshift() 메서드를 통해 추가
    
    ```jsx
    <input onChange={(e)=> {
      입력값변경(e.target.value)
      
    }}/>
    <button onClick={()=> {
      let title = [입력값,...글제목]
      글제목함수(title)
    }}>저장</button>
    ```
    
2. 글마다 삭제버튼 & 삭제 하기
    1. 고민을 조금했는데 그냥 filter() 메서드를 사용하여 현재 map() 메서드로 돌아서 
     얻게되는 article 값이 있기 때문에 해당 값과 같지 않은 것들을 변수에 담아주도록 하고
         글제목함수를 통해 state변경해주기
        1. 추가> 강사님이 하는 방법은
            1. title.splice(i, 1)로 splice() 메서드로 삭제했음
    
    ```jsx
    {
      글제목.map((article,i)=> {
        return (
          <div>
            <h1 onClick={()=> {
              let title = article
              선택글제목변경(title)
              setModal(true)
            }}>{article} <span style={{cursor: 'pointer'}} onClick={(e)=> {
              e.stopPropagation()
              let thumb = [...따봉]
              thumb[i] = 따봉[i] +1
              따봉변경(thumb)
            }}>👍</span>{따봉[i]}</h1>
            <div>{글제목2[i]} <button onClick={(e)=>{
              let title = [...글제목].filter((t) => {
                return t != article
              })  
              글제목함수(title)
            }}>삭제</button></div>
          </div>
        )
      })
    }
    ```
    

여기서 추가로 더 시도 해본것으로

1. 작성 후 해당 input 태그의 value를 빈칸으로 초기화 하기
    1. DOM을 이용해서 id에 해당하는 input 태그를 지정후 해당 태그를 ‘’으로 변경
    
    ```jsx
    else {
      let title = [입력값,...글제목]
      let inp = document.getElementById('input')
      inp.value = ''
      글제목함수(title)
    }
    ```
    
2. 저장 버튼 클릭이 아니어도 Enter 버튼을 누르게 되면 저장이 될 수 있도록 하기
    1. 우선 button 태그에서 많은 시도를 해봤는데 결국에는 input 태그로 해결을 했고
    2. input태그에서도 type을 submit으로 해서 onSubmit으로도 해보고 했지만 잘 안되었다.
    3. 그래서 결국 해결한 방법은 type을 없애고 onKeyDown의 event를 가져와서
     해당 event의 key가 Enter의 경우 실행되도록 하여 해결
    
    ```jsx
    <input id="input" onChange={(e)=> {
            입력값변경(e.target.value)
            console.log(입력값);
          }} onKeyDown={(e)=> {
            if (e.key === 'Enter') {
              console.log(e.key);
              if (입력값 === ''){
                alert('경고')
              }
              else {
                let title = [입력값,...글제목]
                let inp = document.getElementById('input')
                inp.value = ''
                글제목함수(title)
              }
            }
          }} />
    ```
    
3. 그리고 입력칸이 빈칸일 경우 저장되지 않도록 하기 
    1. 이것은 간단했다 그냥 현재 입력값이라고 하는 state의 값이 ‘’ 이렇게 비워져있다면
     alert 처리를 해주는 것으로 해결
    
    ```jsx
    if (입력값 === ''){
      alert('경고')
    }
    ```
    
    ---
    
    `1207`
    
    클래스 문법으로 컴포넌트를 만드는 방법
    
    우선 class는 변수, 함수 보관함으로 생각하면 된다.
    
    - 리엑트에서는 우선적으로 채워줘야하는 것이 아래와 같다
     (그냥 template처럼 생각하면 된다.)
        - constructor
        - super
        - render
    - 그래서 아래와 같이 작성하게 되면 Modal2를 작성하는 것만으로 
     긴 HTML을 작성할 수 있게 된다.
       
        ```jsx
        class Modal2 extends React.Component {
          constructor() {
            super()
          }
          render() {
            return (
              <div>안녕</div>
            )
          }
        }
        ```
       
    - 해당 클래스는 App 의 최상단 태그 안에 작성해야 작성이 된다.

- 그래서 현재 사용하는 Component와 Class를 통해 만든 Component 작성을 비교하면
 아래와 같다

```jsx
// 현재
function Modal(props) {
  return (
    <div className="modal" style={{backgroundColor:props.color}}>
      <h2 id="title">{props.선택글제목}</h2>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  );
}

// class를 통해 만든 Component
class Modal2 extends React.Component {
  constructor() {
    super()
  }
  render() {
    return (
      <div>안녕</div>
    )
  }
}

```

- class를 통해 만든 컴포넌트에서의 state만드는 방법

```jsx
class Modal2 extends React.Component {
  constructor() {
    super();
    this.state= {
      name: 'kim',
      age: 20
    }
  }
  render() {
    return (
      <div>안녕</div>
    )
  }
}
```

- state적용
 꼭 가장 최상단 태그 안에 작성을 해야 한다.

```jsx
class Modal2 extends React.Component {
  constructor() {
    super();
    this.state= {
      name: 'kim',
      age: 20
    }
  }
  render() {
    return (
      <div>
        안녕 {this.state.name}

      </div>
      
    )
  }
}
```

- 기존의 state 값을 변경하고자 할 경우 
 아래와 같이 this.setState({변수: 변경값}) 이렇게 변경해주면 된다.

```jsx
class Modal2 extends React.Component {
  constructor() {
    super();
    this.state= {
      name: 'kim',
      age: 20
    }
  }
  render() {
    return (
      <div>
        안녕 {this.state.name}
        <button onClick={()=> {
          this.setState({name:'hongmin'})
        }}>버튼</button>
      </div>
      
    )
  }
}
```

- 그리고 props를 하고자 할 경우엔

```jsx
class Modal2 extends React.Component {
  constructor(props) {
    super(props);
    this.state= {
      name: 'kim',
      age: 20
    }
  }
  render() {
    return (
      <div>
        안녕 {this.props}
        <button onClick={()=> {
          this.setState({name:'hongmin'})
        }}>버튼</button>
      </div>
      
    )
  }
}
```

---

font 적용

로컬에 다운로드한 폰트를 적용하는 방법

- react에 assets 폴더를 만든다
- font라는 폴더를 만들어 정리를 한번 더 해준다

```jsx
// css 파일을 생성

@font-face {
	font-family: '해당 폰트를 불러올 이름 작성(웬만하면 원래 이름 적어주기)'
	src: url('현재 파일이 있는 경로')
}

// 적용하는 방법
font-family: '해당 폰트 이름'
```

---

`1210`

새로운 리엑트 프로젝트 생성

기존의 blog 폴더가 있는 곳에서의 상위 폴더에서 

shift + 마우스 우클릭 을 하게 되면 여기서 powerShell 창 열기가 나오게 되고 클릭하면 된다.

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2018.png)

이후 PowerShell에서 npx create-react-app {프로젝트 이름} 을 작성하게 되면 프로젝트가 생성된다.

*React에서 Bootstrap 사용하기*

우선 구글에 react bootstrap을 입력하면 상단에 나오는 홈페이지에서 
 cdn같은 걸 복사 후 터미널에서 실행 시키고

 페이지 하단에 있는 CSS 부분에서 App.js 에 넣을 import 도 함께 넣어주자.

이후 만약 버튼을 하나 넣으려고 할때

```jsx
아래와 같은 코드만 넣어준다고 해서 되는 것이 아니라 component이기 때문에
 react bootstrap 홈페이지에서 importing Components부분을 참고하여 import또한 같이 해줘야한다.
<Button variant="primary">Primary</Button>{' '}

```

/*여기서 문제점*/

리엑트에서 부트스트랩을 사용하려 할 경우 !important 때문인지 해당 태그 안에서 
 style을 먹이지 않으면 css가 먹지 않는 것 같다.

 css파일 내에서 적용을 하려해도 안되는게 무슨 이유일까…?

background-image 속성

url() 주소를 넣어주어 해당 경로를 입력해주고

background-position 속성을 통해 해당 배경 사진의 위치를 변경할 수 있다.

그리고 css 파일 상에서는 위의 방법과 같이 작성해주면 되지만

App.js 즉 html에서 src폴더의 이미지를 넣을 땐

상단에 import {작명} from {이미지 경로} 와 같이 경로를 받아온후

style={{ backgroundImage:’url( ‘+작명+’ )’ }} 과 같이 해줘야한다.

 **주의할점**

꼭 backgroundImage: ‘ url ( ’ + 작명 + ‘ ) ‘  이렇게 해줘야한다는것

다음으로 하단에 3개의 사진을 넣어주기

궁금했던 부분:
Q. 왜 그냥 bootstrap을 사용하지 않고 react bootstrap을 사용할까?  

A. 조금 더 용량 절약이 가능하기 때문

html에서 img 파일을 불러올 때 위의 방식대로 하게 되면 

너무 번거롭고 불편하기에

public 파일에 넣고 사용을 하기도 한다.

그래서 public 폴더에 있는 이미지를 사용할 경우

그냥 / 하나면 하고 바로 파일 명을 작성하면 사용이 가능하다

단 위의 방법을 사용할 경우 주의할 점

메인 페이지가 아닌 다른 경로에서 사용할 경우 조금 번거로워진다.

ex) <img src={process.env.PUBLIC_URL + ‘/img/logo,png’} />

금일 만든 페이지

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2019.png)

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2020.png)

---

`1211`

DB가 아닌 그냥 현재 React에서 데이터를 넣은 후 값을 가져오고자 할 때

App.js 내부에서 하기에는 너무 코드가 길어지니까 다른 파일에서 불러오고자 할 경우!

1. 먼저 src폴더 내부에 ex) data.js 파일을 생성 후 
2. 해당 파일에서 데이터를 export하고
   
    ```jsx
    // 만약 변수 a를 export 하려고 한다면
    let a = 10
    
    export default a
    
    ```
    
3. App.js에서 import하면 끝
   
    ```jsx
    // App.js 파일에서 아래와 같이 코드를 작성하면 끝
    
    import 작명 from './data.js' 
    ```
    

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2021.png)

**여기서 만약에 여러 개를 export 시키려 한다면**

```jsx
// data/js

let a = 10
let b = 100

// 아래와 같이 중괄호로 감싸줘야한다.
export {a,b}
```

여기서 import를 하는 App.js에서는 아래와 같이 작성해야한다.

```jsx
// App.js

import {a,b} from './data.js'
```

단 여러개를 export 했을 경우 import 할 경우 작명을 하나만 export 했을 때처럼 
자유롭게 할 수 없고 export 했을 때의 변수 그대로 사용해야 한다.

그리고 함수,모달 또한 export 가능하다!!

**과제**

1. 상품 목록 컴포넌트화
   
    ```jsx
    import {Navbar,Nav} from 'react-bootstrap';
    
    let nav = [
      <Navbar id='navbar' variant="dark">
        <div className="grid subfont">
          <div className=''></div>
          <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }} href="#home"><span class="material-symbols-outlined" style={{marginRight:'3px'}}>menu</span>메뉴</Nav>
          <div></div>
          <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }}  href="#features"><span class="material-symbols-outlined">search</span>검색</Nav>
          <div></div>
          <Nav className='mainfont' style={{color:'black',justifyContent: 'center',alignItems: 'center', fontSize:'2rem', letterSpacing:'5px'}}  href="#home" >LOUIS VUITTON</Nav>
          <div></div>
          <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }}  href="#home" >위시리스트</Nav>
          <div></div>
          <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }}  href="#pricing">My lv</Nav>
          <div></div>
          <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }}  href="#pricing"><span class="material-symbols-outlined">shopping_cart_checkout</span></Nav>
        </div>
      </Navbar>
    ]
    ```
    
2. 상품명 데이터 바인딩도 잘 해오기
   
    ```jsx
    
    let data = [
      {
        id : 0,
        title : "White and Black",
        content : "Born in France",
        price : 120000
      },
    
      {
        id : 1,
        title : "Red Knit",
        content : "Born in Seoul",
        price : 110000
      },
    
      {
        id : 2,
        title : "Grey Yordan",
        content : "Born in the States",
        price : 130000
      }
    ]
    
    let items = [
      <div style={{marginRight:'4px'}}>
        <img className='items' src="https://images.pexels.com/photos/4602025/pexels-photo-4602025.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="" />
        <p style={{marginTop:'7px'}}>{data[0].title}</p>
        <p>{data[0].content}</p>
      </div>,
      <div style={{marginRight:'4px', marginLeft:'2px'}}>
        <img className='items' src="https://images.pexels.com/photos/4276653/pexels-photo-4276653.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="" />
        <p style={{marginTop:'7px'}}>{data[1].title}</p>
        <p>{data[1].content}</p>
      </div>,
      <div style={{marginLeft:'4px'}}>
        <img className='items' src="https://images.pexels.com/photos/4061385/pexels-photo-4061385.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="" />
        <p style={{marginTop:'7px'}}>{data[2].title}</p>
        <p>{data[2].content}</p>
      </div>
    ]
    ```
    
3. 반복적인 부분은 map 반복문 써보기
    1. array helper method의 경우엔 map을 예시로 들어본다면 
    2. array.map() 이렇게 그냥 배열 형태인 곳 어디에든 사용하면 되는거 같다.
    
    ```jsx
    <div className='contain'>
      <div></div>
      {item.map((item) => {
        return item
      })}
      <div></div>
    </div>
    ```
    

위와 같이 data를 export 하고 import 하여 App.js에서 사용하다 보니 엄청 깔끔 해졌다.

```jsx
import './App.css';
import React ,{useState} from 'react';
import 'bootstrap/dist/css/bootstrap.min.css';
import {nav, items} from './data.js'

function App() {

  let [item, setItems] = useState(items)

  return (
    <div className="App">
      {/* navbar */}
      {nav}
      
      <div className='main-bg'>
        {/* 배경사진 */}
      </div>

      <div className='contain'>
        <div></div>
        {item.map((item) => {
          return item
        })}
        <div></div>
      </div>
    </div>
  );
}

export default App;
```

props 다시 한번 정리

```jsx
// component에 data를 props 시키려고 할 때
<component data={data}> </compoenent>
```

**강사님이 의도한 거??**

```jsx
-------------------------------------------------------------------------------------
// 강사님이 의도한 바는 조금 다른거 같다
// App.js 내에서 아래의 코드를 작성해서 컴포넌트를 만드는 것으로 의도 하셨다.

function Card() {
  return (
    <div style={{marginRight:'4px'}}>
      <img className='items' src="https://images.pexels.com/photos/4602025/pexels-photo-4602025.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="" />
      <p style={{marginTop:'7px'}}>{data[0].title}</p>
      <p>{data[0].content}</p>
    </div>
  )
}

// 이후 현재 Card 라는 컴포넌트 내부엔 datas 라는 데이터가 없기 때문에 
// App컴포넌트에서 자식 컴포넌트인 Card 컴포넌트에게 props를 해줘야해서
// App컴포넌트 태그 안에 Card 컴포넌트 생성 후 props 해주기

<div>
  <Card data={data}></Card>
</div>

// 다만 여러개의 컴포넌트를 가져올 예정이기에 위의 코드로 3개를 만든다면 아래처럼 될텐데
<div>
  <Card data={data}></Card>
	<Card data={data}></Card>
	<Card data={data}></Card>
</div>

// 이렇게 되면 같은 data[0] 의 데이터만 조회하게 되기 때문에 
<div>
  <Card data={data[0]}></Card>
	<Card data={data[1]}></Card>
	<Card data={data[2]}></Card>
</div>

function Card() {
  return (
    <div style={{marginRight:'4px'}}>
      <img className='items' src="https://images.pexels.com/photos/4602025/pexels-photo-4602025.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="" />
      <p style={{marginTop:'7px'}}>{data.title}</p>
      <p>{data.content}</p>
    </div>
  )
}

// 이렇게 작성해주면 각자 다른 data의 title과 content가 조회된다.
// 다만 이미지가 서로 다르게 되는데 이때 만약 서로 유사한 이미지 주소 혹은 파일명의 경우엔
// props로 해당 데이터에 맞는 숫자를 함께 props 해주고 데이터를 변경해주면 된다.
// 예를 들어 이미지 주소가 아래와 같을 경우
// https://codingapple1.github.io/shop/shoes1.jpg
// https://codingapple1.github.io/shop/shoes2.jpg
// https://codingapple1.github.io/shop/shoes3.jpg
// props 할때 함께 숫자도 넘겨주기

<div>
  <Card data={data[0]} i={1}></Card>
	<Card data={data[1]} i={2}></Card>
	<Card data={data[2]} i={3}></Card>
</div>

// 이후 주소 또한 함께 변경하자면
// 먼저 src속성을 자바스크립트 입력란으로 변경해주고 {} => 문자열로 변경 '' 이후
// props 할 부분과 문자열인 부분을 나누어 + + 처리 해주어 처리 (문자 중간 변수 넣기 문법)
function Card() {
  return (
    <div style={{marginRight:'4px'}}>
      <img className='items' 
			src={'https://codingapple1.github.io/shop/shoes' + props.i + '.jpg'} alt="" />
      <p style={{marginTop:'7px'}}>{data.title}</p>
      <p>{data.content}</p>
    </div>
  )
}

// 그리고 map()함수를 이용해서 컴포넌트를 보이도록 하는 방법
// 위와 같이 작성하게 되면 계속 변화하는 변수의 경우엔 
// 시시각각으로 변경을 해야하기에 손이 많이 간다 그래서 반복문을 통해 다 보여주도록 하기

// map()함수를 작성할 때는 {}중괄호 안에다가 작성하기
// 우선 사진의 경우엔 지금은 조금 맞지는 않지만 이렇게도 가능하다는 것!
{
  data.map((data, idx)=> {
    return (
      <Card data={data} i={4602025-idx}></Card>
    )
  })
}
```

---

`1212`

리액트 라우터

리엑트에서 페이지 나누는 법

1. 컴포넌트를 만들어서 상세페이지 내용 채우기
2. 누가 /detail에 접속하면 해당 커포넌트를 보여줌

설치 순서

1. terminal → npm i react-router-dom@6
2. index.js → BrowserRouter 를 작성하기
    1. import 또한 함께 해주고 BrowserRouter 태그로 App을 감싸주기

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2022.png)

외부라이브러리 사용하는 방법(일반적으로는 검색해서 찾으면 된다)

라우터의 경우엔 App.js의 상단에 import로 불러오기

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2023.png)

라우터로 페이지 나누는 법

예를 들어 우리 사이트에 페이지가 4개가 필요할 것 같다면

아래 사진과 같이 Routes 컴포넌트 안에 Route 컴포넌트를 4개 넣어주면 된다. 

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2024.png)

그리고 만약 경로가 /detail 인 곳으로 이동할 페이지의 경우엔 아래와 같이 작성하고

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2025.png)

그리고 해당 페이지안의 요소를 작성하려면 아래와 같이 작성하면 된다.

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2026.png)

해당 경로로 이동하게 되면

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2027.png)

만약 메인페이지를 꾸미고 싶을 경우엔 path를 / 만 적어두면 된다.

```jsx
<Routes>
  <Route path='/' element={<div>메인페이지임</div>} />
</Routes>
```

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2028.png)

그리고 팁으로 react에서는 태그로 감싼뒤 요소들을 넣어야 하기 때문에 

이때 div태그를 적기 그렇다면 그냥 <> </>만 넣어줘도 된다. 

무튼 해당 element 속성 안에 원하는 데이터를 <></> 태그 혹은 다른 태그로 감싼 상태로

넣어주게 되면

```jsx
<Routes>
  <Route path='/' element={<>
  <div className='main-bg'>
  {/* 배경사진 */}
  </div></>} />

  <Route path='/detail' element={<>
    <div className='contain'>
      <div></div>
      {item.map((item) => {
        return item})}
      <div></div>
    </div></>}/>
</Routes>
```

main 페이지

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2029.png)

detail 페이지

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2030.png)

페이지 이동 버튼

Link 태그 사용하기 

- to 속성을 이용해서 기존에 작성했던 path 경로로 이동할 수 있도록 해준다.

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2031.png)

![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2032.png)

숙제

- 상세페이지 컴포넌트로 만들어오기
    - 너무 길면 다른 파일로 빼서 가져오도록 해보기

우선 나는 내가 원하는 사이트를 만들기 위해 

한번 작성만 해보고 사용하지 않을거라서 

다른 파일에서 작성후 export 해서 App.js 에서 import 하여 사용하는 형식으로 했다.

1. 새로운 파일에서 데이터를 작성후 export 하기
    1. js 파일이기 때문에 파이썬에서 처럼 그냥 변수를 선언하는 것이 아닌 
     let, const, var 로 지정해줘야 한다는것.
    2. export 할때 
        1. 하나면 default 해주고
        2. 여러개면 default 없이 {} 중괄호 안에 작성해주기 
    
    ```jsx
    let comp = [
      <div className="container">
      <div className="row">
        <div className="col-md-6">
          <img src="https://codingapple1.github.io/shop/shoes1.jpg" width="100%" />
        </div>
        <div className="col-md-6">
          <h4 className="pt-5">상품명</h4>
          <p>상품설명</p>
          <p>120000원</p>
          <button className="btn btn-danger">주문하기</button> 
        </div>
      </div>
    </div> 
    ]
    
    export default comp
    ```
    
2. App.js에서 사용하기
    1. 사용할때는 import 해줘야하는데 
        1. 데이터가 하나의 경우엔 변수값을 아무거나 줘도 괜찮지만 
        2. 여러개의 경우엔 지정했던대로 해줘야 한다는것.
    2. <Routes></Routes> 태그 안에 <Route /> 를 작성한다는 것
    3. <Route /> 속성으로는 path, element 가 있다는 것
    4. 해당 경로로 가기 위해 사용하는 <Link></Link> 태그에는
        1. Route에서 지정했던 path로 가기 위한 to 속성이 있다.
        
        ```jsx
        import comp from './newcomponent'
        
        <Link to={'/comp'}>새로운 컴포넌트</Link>
        
        <Route path='/comp' element={<>
          {comp}
        </>}/>
        ```
        
        ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2033.png)
        
    
    여기서 내가 잘못 생각햇던 부분
    
    컴포넌트를 만든다고 하는 것은 함수 형식으로 만드는 것이라는 것.
    
    내가 한 것은 그냥 데이터를 전달한것이라는 거…
    
    그래서 원래 컴포넌트를 만드는 것을 하려면
    
    ```jsx
    function Comp() {
      return (
        <div className="container">
          <div className="row">
            <div className="col-md-6">
              <img src="https://codingapple1.github.io/shop/shoes1.jpg" width="100%" />
            </div>
            <div className="col-md-6">
              <h4 className="pt-5">상품명</h4>
              <p>상품설명</p>
              <p>120000원</p>
              <button className="btn btn-danger">주문하기</button> 
            </div>
          </div>
        </div> 
      )
    }
    
    export default Comp 
    ```
    
    사용할때는 
    
    ```jsx
    // App.js
    
    import Comp from './newcomponent'
    
    import comp from './newcomponent'
    
    <Link to={'/comp'}>새로운 컴포넌트</Link>
    
    <Route path='/comp' element={<>
      { <comp />}
    </>}/>
    ```
    
    **navigate, nested routes, outlet**
    
    1. 페이지 이동을 도와주는 useNavigate()
        1. 사용 할 때는
        
        ```jsx
        let navigate = useNavigate()
        ```
        
        1. useNavigate()를 사용하는 이유
            1. 기존의 Link태그의 경우 a태그처럼 생겼기때문에 내가 클릭한 것을 통해 
             원하는 경로로 이동하고자 할 경우 사용한다고 한다. (그냥 Link는 a태그 같아서??)
            2. 그리고 만약 다른 파일에서 export 해서 사용할 경우 적용이 안되는 것 같은데
             (더 찾아봐야할 듯)
                ex) data.js에서 작성한 nav에서 navigate를 사용할 경우 해당 페이지에선 
                     path가 적힌곳이 없기에 에러가 뜬다.
            3. 그래서 기존 data.js에서 작성한 데이터를 App.js로 다시 옮겨왔음 
            
            ```jsx
             <Navbar id='navbar' variant="dark">
                    <div className="grid subfont">
                      <div className=''></div>
                      <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }} href="#home"><span class="material-symbols-outlined" style={{marginRight:'3px'}}>menu</span>메뉴</Nav>
                      <div></div>
                      <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }}  href="#features"><span class="material-symbols-outlined">search</span>검색</Nav>
                      <div></div>
                      <Nav className='mainfont' style={{color:'black',justifyContent: 'center',alignItems: 'center', fontSize:'2rem', letterSpacing:'5px', cursor: 'pointer' }} onClick={()=> {navigate('/')}}>LOUIS VUITTON</Nav>
                      <div></div>
                      <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center', cursor: 'pointer' }}  onClick={()=> {navigate('/detail')}} >위시리스트</Nav>
                      <div></div>
                      <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }}  href="#pricing">My lv</Nav>
                      <div></div>
                      <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center' }}  href="#pricing"><span class="material-symbols-outlined">shopping_cart_checkout</span></Nav>
                    </div>
                  </Navbar>
            ```
            
        
        ```jsx
        // 간단하게 정리하자면
        import {useNavigate} from 'react-router-dom';
        
        let navigate = useNavigate()
        
        function App() {
        	return(
        		<div onClick={()=>{navigate('/')}}>Home</div>
        
        		<Routes>
        			<Route path='/' element="<><div>여긴 홈</div></>"/>
        		</Routes>
        	)
        }
        ```
        
        그리고 다음 페이지, 이전 페이지 
        
        navigate( 1 ) 은 한 페이지 앞으로 가기가 되고
        
        navigate( -1 ) 은 한 페이지 전으로 가게 된다.
        
        물론 (2) 를 넣으면 두 페이지 앞과 전으로 이동하게 된다.
        
        404페이지
        
        Vue에서와 마찬가지로 path를 ‘ * ’ 아스타리스크 즉 별표로 해놓으면 된다. 
        
        다만 Vue와는 다르게 가장 하단에 적지 않아도 잘 작동 하는듯..? 내가 몰라서 그런가?
        
        따로 강사님이 언급은 안함
        
        ```jsx
        <Route path='*' element={<>여긴 뭐하러 왔어?</>}/>
        ```
        
        ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2034.png)
        
        Nested Routes
        
        우선 About 컴포넌트가 있는 페이지로 이동하고자 할 경우를 설정
        
        ```jsx
        <Nav style={{color:'black',justifyContent: 'center',alignItems: 'center', cursor: 'pointer' }}  onClick={()=>{navigate('/about')}}>My lv</Nav>
        
        <Route path='/about' element={<><About /></>}/>
        
        function About() {
          return (
            <div>
              <h4>회사정보임 ㅅㄱ</h4>
            </div>
          )
        }
        ```
        
        그런데 여기서 경로를 ‘ /about ‘ 말고 ‘ /about/member ‘ 혹은  ‘ /about /location‘ 으로 가는 
         페이지를 만들고자 할 경우
        
        물론 아래와 같이 작성해도 되긴하다.
        
        ```jsx
        <Route path='/about' element={<><About /></>}/>
        <Route path='/about/member' element={<><About /></>}/>
        <Route path='/about/location' element={<><About /></>}/>
        ```
        
        더 유용하게 사용되는 것으로는 Nested Routes 가 있다.
        
        이때는 <Route / > 이렇게 사용하지 않고
        <Route> </Route> 이렇게 닫는 태그를 사용하며 안에 품는 경로만 작성해주기.
        
        ```jsx
        <Route path='/about' element={<><About /></>}> 
        	<Route path='member' element={<> <div>안녕</div> </>}/>
        	<Route path='location' element={<><About /></>}/>
        </Route>
        ```
        
        장점1. Route 작성이 비교적 간단해지게 된다.
        
        장점2. nested route 접속시엔 element가 2개나 보이게 된다.
        
        ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2035.png)
        
        그런데 두개다 보여지지 않게 되고 하나만 보이게 되는데 
        
        이럴때 사용하는 것이 
        
        <Outlet></Outlet> 인데 이것은 구멍을 뚫어 놓음으로써 
        
        nested route가 들어올 구멍을 미리 만들어 주는 것이다.
        
        ```jsx
        function About() {
          return (
            <div>
              <h4>회사정보임 ㅅㄱ</h4>
              <Outlet></Outlet>
            </div>
          )
        }
        ```
        
        ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2036.png)
        
        이제야 보이게 된다.
        
        정리 
        
        Nested Routes 는 언제 사용하는가??
        
        - 여러 유사한 페이지가 필요할 때
        
        Route의 장점
        
        - 페이지의 앞 뒤로 가기 버튼 이용가능
        - 페이지 이동이 쉬움
        
        ---
        
        `1214`
        
        상세페이지에 상품명 넣기
        
        뭐가 좀 이상해졌는데 …
        
        무튼 현재 Detail 컴포넌트는 따로 만들지 않고 해당 코드를 Route안의 element에 넣었는데
        
        갑자기 강사님은 따로 파일을 빼서 정리를 해뒀다.
        
        우선 App에서 Detail로 item 데이터를 전송하기 위해서 props를 이용
        
        ```jsx
        <Route path='/detail' element={<Detail item={item} />}/>
        ```
        
        ```jsx
        function Detail(props) {
          return (
            <div className='contain'>
              <div></div>
              {props.item.map((item) => {
                return item})}
              <div></div>
            </div>
          )
        }
        
        export default Detail
        ```
        
        근데 여기서 
        
        Q. Detail.js 안에 item이라는 state를 하나 더 만들어주고 props를 하지 않으면
              더 편하지 않음??
        
        이렇게 되면 앞서 프젝했을 때처럼 당황스러운 결과가 나오게 되는데
        
        데이터의 수정사항이 생겼을 때 
        예를 들어 데이터를 DB에 넣고 수정하고 조회 할 경우 문제가 생기게 된다.
        
        그래서 꼭 데이터는 한곳에서 보관을 해야한다.
        
        그리고 현재는 디테일 페이지에 모든 item에 대한 요소를 보여주고 있는데 
        
        원래 디테일 페이지의 의도로는 하나의 요소에 대한 정보만 보여주기를 원한다
        
        그렇기에 의도대로 보이게 하려면 아래와 같이 작성을 해야하는데
        
        ```jsx
        <Route path="/detail/0" element={<Detail item={item[0]} />}
        <Route path="/detail/1" element={<Detail item={item}[1] />}
        <Route path="/detail/2" element={<Detail item={item}[2] />}
        ```
        
        만약 여기서 요소가 100개 1000개 이렇게 엄청나게 많다면 힘들어질것이다.
        
        그래서 사용할 수 있는 방법은 뭐 반복문도 있겠지만
        
        Route적으로 해결하는 방법이 있다고 한다.
        
        해결방법
        
        페이지를 여러개 만들고 싶을 경우
        
        - URL 파라미터 ( :id 와 같이 작명)
            - 이렇게 할경우 /detail/아무거나 라는 의미가 된다.
            - 참고로 URL 파라미터는 여러개 사용가능하다.
        
        ```jsx
        <Route path="/detail/:id" element={<Detail item={item[0]} />}
        ```
        
        다만 위의 코드로 작성하게 되면 
        
        페이지의 내용은 모두 똑같은 내용으로 보이게 된다.
        
        그래서 해결하는 방법으로는 유저가 URL 파라미터에 입력한것을 가져와야하는데
        
        그 방법은 useParams() 를 사용하는 것.
        
        useParams는 :id 라고 작명한 URL파라미터 값을 가져오게 된다.
        
        ```jsx
        import { useParams } from "react-router-dom"
        import {datas} from './data'
        
        function Detail(props) {
        
          let {id} = useParams()
          
          return (
            <div className="contain">
              <div style={{marginRight:'4px'}}>
                <img className='items' src="https://images.pexels.com/photos/4602025/pexels-photo-4602025.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" alt="" />
                <p style={{marginTop:'7px'}}>{datas[id].title}</p>
                <p>{datas[id].content}</p>
              </div>
            </div>
          )
        }
        
        export default Detail
        ```
        
        만약 사용자가 없는 숫자나 문자를 입력할 경우엔
        
        if문을 이용해서 없다는 UI를 보여주면 된다.
        

오늘의 응용

- App.js에서 정렬버튼을 눌렀을 때 정렬해주기
- /detail/0 접속시 0번째 상품말고 상품 id가 0인걸 보여주면 좋을 듯

일어나면 할것

과제하기 전에 데이터 강사님이 올려준거로 변경해놓자 귀찮다…

---

`1215`

우선 뭔가 많이 싹 갈아 엎었는데

1. 데이터 자체를 먼저 변경했다.
    1. 기존의 내가 임의로 넣은것에서 강사님이 올린 데이터로 변경
    
    ```jsx
    let datas = [
      {
        id : 0,
        title : "White and Black",
        content : "Born in France",
        price : 120000
      },
    
      {
        id : 1,
        title : "Red Knit",
        content : "Born in Seoul",
        price : 110000
      },
    
      {
        id : 2,
        title : "Grey Yordan",
        content : "Born in the States",
        price : 130000
      }
    ] 
    
    let items = [
      <div style={{marginRight:'4px'}}>
        <img className='items' style={{height:'70%'}} src="https://codingapple1.github.io/shop/shoes1.jpg" alt="" />
        <p style={{marginTop:'7px'}}>{datas[0].title}</p>
        <p>{datas[0].content}</p>
      </div>,
      <div style={{marginRight:'4px', marginLeft:'2px'}}>
        <img className='items' style={{height:'70%'}} src="https://codingapple1.github.io/shop/shoes2.jpg" alt="" />
        <p style={{marginTop:'7px'}}>{datas[1].title}</p>
        <p>{datas[1].content}</p>
      </div>,
      <div style={{marginLeft:'4px'}}>
        <img className='items' style={{height:'70%'}} src="https://codingapple1.github.io/shop/shoes3.jpg" alt="" />
        <p style={{marginTop:'7px'}}>{datas[2].title}</p>
        <p>{datas[2].content}</p>
      </div>
    ]
    
    export {items, datas}
    ```
    
2. 디테일 페이지 변경
    1. 원래는 이상하게 디테일 페이지에도 Item 들을 모두 넣은 페이지로 만들어 놨었어서
    2. 새롭게 변경한 페이지로는 해당 아이템 하나에 대한 페이지로 만들어놨다.
    
    ```jsx
    import { useParams } from "react-router-dom"
    import {datas} from './data'
    
    function Detail(props) {
    
      let {id} = useParams()
    
      let data = props.datas.find((data)=> {
        console.log(data);
        return data.id === Number(id)
      })
    
      let dataId = data.id+1
    
      return (
        <div style={{display:'flex', justifyContent:'center',alignItems:'center'}}>
          <div style={{marginRight:'4px'}}>
            <img className='items' style={{height:'50%'}} src={'https://codingapple1.github.io/shop/shoes' + dataId +'.jpg'} alt="" />
            <p style={{marginTop:'7px'}}>{datas[data.id].title}</p>
            <p>{datas[data.id].content}</p>
          </div>
        </div>
      )
    }
    
    export default Detail
    ```
    
3. 그리고 App.js내의 해당 버튼을 누르면 우선 현재 item에 대한 리스트 정렬을 
 reverse() 하도록 해서 버튼을 클릭시 보여지는 Item을 내림차순으로 정렬
    
    ```jsx
    let [item, setItems] = useState(items)
    
    <button onClick={() => {
            let newitem = [...item]
            console.log(newitem);
            newitem.reverse()
            console.log(newitem);
            setItems(newitem)
          }}>
            반전 버튼
          </button>
    ```
    
4. 강사님이 내준 과제해결로는 useParams()를 사용해서 주소창에 입력한 값을 id라는 변수에 넣고
    props를 해온 data에 해당 하는 id와 useParams의 값을 담은 변수 id와 일치 하다면 찾아내는
    find array helper method를 사용하여 변수에 담아 보이도록 하였음.
    1. 여기서 useParams를 담는 변수의 이름은 중괄호로 감싸줘야하는 것 같다.
    
    ```jsx
    import { useParams } from "react-router-dom"
    import {datas} from './data'
    
    function Detail(props) {
    
      let {id} = useParams()
    
      let data = props.datas.find((data)=> {
        console.log(data);
        return data.id === Number(id)
      })
    
      let dataId = data.id+1
    
      return (
        <div style={{display:'flex', justifyContent:'center',alignItems:'center'}}>
          <div style={{marginRight:'4px'}}>
            <img className='items' style={{height:'50%'}} src={'https://codingapple1.github.io/shop/shoes' + dataId +'.jpg'} alt="" />
            <p style={{marginTop:'7px'}}>{datas[data.id].title}</p>
            <p>{datas[data.id].content}</p>
          </div>
        </div>
      )
    }
    
    export default Detail
    ```
    
    styled-components 사용하기
    
    - npm install styled-components
    - 사용할 곳에서 import 해오기
      
        ```jsx
        import styled from 'styled-components'
        ```
        

styled-components 를 사용하는 이유

- 기존에 버튼을 하나 생성하고 꾸민다면 className을 넣고 CSS파일에 가야한다.
  
    ```jsx
    <button className='???'>버튼</button>
    ```
    
- 그런데 styled-components를 사용하면 JS파일에서 전부 해결이 가능하다.

사용하는 방법

- 사용하려는 곳에서 임의의 변수에다가 styeld 이후 생성하고자 하는 태그를 작성후 
  ` ` 백틱 사이에 css넣는 것처럼 작성해주면 된다. (그러면 해당 태그 생성과 동시에 CSS적용)
    - 아래는 버튼 태그 생성
- 사실은 하나의 스타일이 입혀진 컴포넌트를 생성한 것이라고 보면 된다고 한다.
- 여기서 중요한 점은 해당 변수의 이름의 단어별 첫글자는 무조건 대문자로 해야 된다.
  (컴포넌트이기 때문??)
  
    ```jsx
    import styled from 'styled-components'
    
    let YellowBtn = sytled.button`
    	background: yellow;
    	color: black;
    	padding: 10px;
    `
    ```
  
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2037.png)
  
    styled-components 장점
  
    1. CSS파일 열지 않아도 된다는 점.
    2. 스타일이 다른 js파일로 오염되지 않는다.
        1. 여기서 만약에 CSS 파일 자체를 오염되는것을 방지하려면 컴포넌트.module.css 로 작명
           
              ex. App.css ⇒ App.module.css 
                
              이렇게 작명하게 되면 App.css에만 종속되게 된다.  
        
    3. 페이지 로딩시간이 단축된다.
        1. 해당 페이지에 모든것이 다 있기 때문
        

Q. 근데 여기서 노란색 버튼이 아닌 오렌지색 버튼이 필요할 경우엔?

- props 문법을 사용하면 된다.
- 컴포넌트이기 때문에 props를 받아올 수 있다.
    - 그렇기 때문에 props 데이터를 이용하여 컴포넌트를 재활용할 수 있다.
    
    ```jsx
    let YellowBtn = styled.button`
      background: ${ props => props.bg};
      color: black;
      padding: 10px;
    `
    
    <Btn bg={'orange'}>버튼</Btn>
    <Btn bg={'black'}>버튼</Btn>
    ```
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2038.png)
    
- 여기서 props를 하는 방법이 독특한데
    - ${ props ⇒ [props.bg](http://props.bg) }
    - 따로 이해해야 하는 부분은 아니고 외부 라이브러리 사용법이다 보니 그냥 그렇다정도
- 그리고 styled의 백틱 내부에는 JS를 사용하기 때문에 조건문 또한 가능하다.
  
    ```jsx
    let Btn = styled.button`
    	background: ${ props => props.bg }
    	color: ${props = props.bg === blue? 'white': 'black' }
    `
    
    <Btn bg={'orange'}>버튼</Btn>
    <Btn bg={'blue'}>버튼</Btn>
    ```
    
    ![Untitled](React%201c5967022dbd4ed1874b614a787397e5/Untitled%2039.png)
    
    또한 기존의 컴포넌트로 만든 스타일을 복사도 가능하다.
    
    ```jsx
    let NewBtn = styled.button(Btn)`
    	
    `
    ```
    

styled-compoenent 단점

1. JS가 길어질 수록 JS파일이 매우 복잡해진다.
2. 중복스타일은 컴포넌트간 import 할텐데 CSS와 다른 바가 없다.
3. 협업시 CSS담당의 숙련도 이슈

---