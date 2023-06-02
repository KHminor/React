# React 2

`1216`

컴포넌트의 Lifecycle

 

컴포넌트는 언제 보이는가 하면

컴포넌트가 페이지에 장착되는 시기인 Mount 될 때 이다.

그리고 컴포넌트 내에서 state가 조작이 된다라면 Update 될 때 이며

컴포넌트가 필요없는 경우(다른 페이지로 이동했을 경우) 에는 unmount 될 때 이다.

이렇게 컴포넌트는 인생주기(Lifecycle)을 겪게 된다.

그래서 컴포넌트의 Lifecycle을 이해하게 된다면 중간중간에 간섭이 
가능하기 때문에 공부하는 것.

여기서 간섭이라고 하는것은 중간중간 코드를 실행하는 것을 의미한다.

우선 기존에 컴포넌트를 만드는 방법은 아래와 같았다.

```jsx
class Detail2 extends React.Component {
	componentDidMount(){
		// 컴포넌트 mount시 여기 코드 실행됨
	}
	componentDidUpdate(){
		// 컴포넌트 update시 여기 코드 실행됨
	}
	componentWillUnmount(){
		// 컴포넌트 unmount시 여기 코드 실행됨
	}
}

// 위와 같이 작성 후
// 아래와 같이 컴포넌트를 사용했었음
<Detail2></Detail2> 
```

요즘에 사용하는 방법은 아래와 같다.

- 변수 생성하는 것처럼 해당 컴포넌트의 return 전에 생성하면 된다.
- useEffect() 함수를 사용하는것으로 훅을 사용하는 것이라고 한다.
- import {useEffect} from 'react' 이렇게 import 해야 사용이 가능하다.

```jsx
// Detail.js

import {useEffect} from 'react'

function Detail(props) {
	useEffect(()=> {
		// ~~ mount, update시 여기 코드가 실행된다.
		console.log('안녕')
	})
}

```

근데 여기서 실행해보면 두번 실행되게 되는데

React 상에서는 우리가 개발을 할 때 useEffect 안의 코드는 디버깅을 위해 
 두번정도 실행된다고 한다.

만약 한번만 실행되게 되게 하고 싶다면 

index.js 파일에 가서 <React.StrictMode> 없애면 된다고 한다.

물론 지우지 않아도 발행하고 나서의 실제 사이트에서는 

한번만 작동하게 된다. 

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled.png)

다만 useEffect 바깥에 넣어도 똑같이 실행이 되는데

useEffect를 사용하게 되는 이유는??

- 우선 실행 시점이 다르다
    - useEffect 안에 작성한 코드는 Html이 렌더링이 모두 되고 나서 실행을 하게 된다.

```jsx
// 이것을 통해서 사용하는 방법은 
// 예를 들어 해당 다른 작업이 먼저 되고 난 뒤에 실행을 하고 싶은데 
// useEffect가 아닌 바깥쪽에 실행 시간이 긴 코드를 작성을 하게 된다면
// 한참이 지나야 수행되고 그 이후에 Html 코드가 보이게 되는데
// useEffect를 사용하게 되면 시간이 오래 걸리는 코드는 Html이 수행되고 난 이후에 
// 실행을 시킬 수 있기때문에 이런 활용성이 있다.
```

그래서 useEffect 안에 적는 코드들은

- 어려운 연산, 시간이 오래걸리는 연산
- 서버에서 데이터를 가져오는 작업
- 타이머 장착하는 작업
    - JS에서는 setTimeout() 함수를 이용해서 타이머를 장착시킬 수 있다.
    - 예를 들어 1초 이후에 해당 코드를 실행한다고 하면
    
    ```jsx
    setTimeout(() => {
    	// 실행할 코드
    }, 1000)
    ```
    

숙제:

Detail 페이지방문 후 2초 지나면 해당 div태그 숨기기

우선 내가 한 방식은 useEffect()를 사용해서 DOM으로 해당 div태그를 선택후

display를 기존의 block에서 none으로 변경하였다.

```jsx
useEffect(()=> {
  setTimeout(() => {
    const sale = document.getElementById('sale')
    sale.style.display = 'none'
  }, 2000);
})

<div id="sale" className="alert alert-warning">
        2초이내 구매시 할인
      </div>
```

그런데 위의 방식은 나도 하면서 Vue에서도 교수님이 하지 말라고 했던 

Dom으로 접근하는 방식이라 다른 방식으로 하는 것을 희망했는데 

강사님이 하는 방식은 아래와 같다.

- 우선 useState() 를 통해 state에 해당 값이 true의 경우 보여주고
 false의 경우 해당 태그가 보이지 않도록 하는 방식으로
 해당 결과를 나타냈다.

```jsx
// 우선 state를 하나 생성하기
let [alert, setAlert] = useState(true)

// 이후 React에서의 조건문 사용하기 (삼항 연산자 사용)
{
  alert === true 
  ? <div id="sale" className="alert alert-warning">
      2초이내 구매시 할인
    </div>
  : null
}

// 이후 setEffect 사용하며 타이머를 사용하기
useEffect(()=> {
  setTimeout(() => {
    setAlert(false)}, 2000);
})
```

 

Lifecycle과 useEffect 2

다만 위에서 작성했던것 보다 더 정확하게 작성하는 코드 방법이 있는데

useEffect내부에 , [] 를 넣어주는 방법이다.

Dependency 라고 한다.

사용하는 이유는 useEffect의 실행조건을 넣을 수 있는 곳이라고 한다.

```jsx
useEffect(()=> {
  setTimeout(() => {
    setAlert(false)}, 2000);
}, [count])
```

우선 해당 조건이 없을 경우 코드가 실행되는 시간은

컴포넌트가 mount 혹은 update 될 때 실행이 되는데,

Dependency를 사용하게 되면 [ ] 대괄호 안의 state가 변경될 때만 실행이 된다.

다만 mount시 [ ] 안의 state가 변할 때는 실행이 된다.

또한 살짝의 편법으로서 사용하는 방법인데

Dependency를 비워둔 상태로 코드를 실행하게 되면 

mount 시에만 해당 코드가 실행되게 된다.

즉 update시에는 실행되지 않는다는 의미가 된다.

```jsx
useEffect(()=> {
  setTimeout(() => {
    setAlert(false)}, 2000);
}, [])
```

또한 다른 컴포넌트처럼 return 또한 사용할 수 있는데

사용하는 방법이 조금은 다르다

return () 소괄호 안에 작성이 아닌 Arrow function을 사용하여 return문 실행

```jsx
useEffect(()=> {
  setTimeout(() => {
    setAlert(false)}, 2000);
		return () => {
		
		}
}, [])
```

또한 실행되는 시간은 **useEffect 동작 전**에 실행되게 된다.

return을 사용하는 것에 대한 명칭은 **clean up function**이라 한다고 한다.

사용에 대한 예로 타이머를 사용할 때를 상황으로 보자면

만약 Dependency 를 사용하지 않았을 경우에 

해당 페이지를 계속해서 update 혹은 Rendering 하게 되면 

엄청나게 많은 타이머가 생성이 될 텐데 그럴 때 

이전의 타이머는 제거해주세요 라는 형식의 코드를 작성할 수 있게 된다.

이유는 **clean up function이라고 하는 return()⇒ {}**은 useEffect동작 전에 실행하게 되기 때문.

그래서 타이머를 제거하는 방법은 아래와 같다.

return 안에 clearTimeout()함수를 사용해서 변수에 담아둔 timer를 넣어주면 된다. 

```jsx
useEffect(()=> {
  let timer = setTimeout(() => {setAlert(false)}, 2000);
		return () => {
			clearTimeout(timer);
		}
})
```

또 다른 사용의 예는 

서버로 데이터를 요청하는 코드를 많이 작성하게 될텐데 

만약 2초의 경과 시간이 필요한 코드의 경우 

계속해서 새로고침을 통해 시간이 쌓여가게 될 때 

clean up function을 사용하면 된다고 한다.

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%201.png)

참고로 clean up function은 mount시에는 실행되지 않고

unmount(즉 컴포넌트가 삭제 혹은 페이지 이동)시엔 실행된다고 한다.

총정리

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%202.png)

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%203.png)

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%204.png)

숙제

input 태그에 숫자말고 다른거 입력하면 

그러지말라고 안내메세지 띄우기

useEffect 사용해서 해결해보기

해결방법(강사님과 유사하게 했음ㅋ)

우선 input 태그내에 값을 입력할때로 나는 onKeyDown을 했는데 

강사님은 onChange로 했다는 차이점 빼고는 같다.

그래서 변경될 때 마다 위에서 새롭게 작성한 state 변경 함수를 이용하여 

해당 tartget.value 값을 넣어주고 

useEffect를 활용해서 해당 state 값이 변경 될때 마다 해당 조건문을 실행하도록 했다.

 

```jsx
let [inText,setInText] = useState(0)

useEffect(()=> {
  if (isNaN(inText)) {
    alert('문자입력 ㄴㄴ')
  }
}, [inText])

<div>
  <input onKeyDown={(e)=> {
    setInText(e.target.value);
  }} type="text" />
</div>
```

---

`1218`

리엑트에서 서버와 통신하려면 AJAX1

서버에 데이터를 요청

여기서 서버란?

- 부탁하면 진짜로 들어주는 프로그램
- ex. Youtube 서버
    - 동영상 요청하는 진짜 보내주는 프로그램
- ex. 네이버 웹툰 서버
    - 웹툰 요청하면 진짜 보내주는 프로그램
- 서버 개발시 짜는 코드
    - 누가 A 요청하면 A 보내주세요~!
- 단 규격에 맞지 않는 요청을 할 시
    
    ![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%205.png)
    
- 그래서 서버는 아래와 같이 요구함
    
    ![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%206.png)
    

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%207.png)

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%208.png)

서버 개발시 짜는 코드를 한번 더 정리하자면

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%209.png)

그렇다면 이제 GET 요청을 보내볼 것인데

가장 기본적은 GET 요청 방법은 

주소창에 입력을 하는 것.

그래서 사전에 준비되어있던 아래 주소를 주소창에 입력한다면

[](https://codingapple1.github.io/shop/data2.json)

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2010.png)

사진과 같이 JSON 형태로 데이터를 받을 수 있게 된다.

또다른 방법인 자바스크립트 코드로 하는 AJAX 

주소창에 입력하는 것과의 차이점

- 주소창에 GET/POST 요청시 새로고침이 된다.

AJAX를 사용하는 방법에 대한 옵션은 총 3가지가 된다.

1. XMLHttpRequest (예전)
2. fetch() (요즘)
3. axios (외부 라이브러리) ←우리가 사용할 것 (코드의 길이도 짧다)

axios 설치

- terminal창에 입력
    
    ```jsx
    npm install axios
    ```
    
- 사용할 곳에 import 하기
    
    ```jsx
    import axios from 'axios'
    ```
    

버튼 클릭시 axios요청하도록 하기

```jsx
 <div>
  <button onClick={()=> { 
    axios.get('https://codingapple1.github.io/shop/data2.json')
  }}>버튼</button>
</div>
```

AJAX 를 이용한 GET요청은 axios.get( ’ url 주소 ’ )

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2011.png)

AJAX를 통한 해당 요청결과는 axios.get( ’ url 주소 ’ ).then() 

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2012.png)

```jsx
<div>
  <button onClick={()=> { 
    axios.get('https://codingapple1.github.io/shop/data2.json')
    .then((data)=> {data})
  }}>버튼</button>
</div>
```

그래서 데이터를 console.log를 통해 확인해본다면

```jsx
<div>
  <button onClick={()=> { 
    axios.get('https://codingapple1.github.io/shop/data2.json')
    .then((data)=> {console.log(data);})
  }}>버튼</button>
</div>
```

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2013.png)

만약 요청에 실패할 경우엔 .catch()로 콜백함수를 사용하여 작성하면 된다,

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2014.png)

숙제

요청하여 가져온 데이터를 HTML로 보이도록 하기

오늘 과제하면서 계속 헤매었던 부분!!

return () 내부에 array.map()을 사용할 때

계속해서 에러는 안뜨는데 데이터가 나오지 않아서 몇시간을 찾고 헤매고 그랬는데

정말 사소한 부분이었다…

데이터가 안나오는 코드

```jsx
<div style={{display:'flex', justifyContent:'center',alignItems:'center'}}>
  {data.map((data)=> {<Datas data={data} />})}
</div>
```

항상 arrow function을 사용할 때는 중괄호를 사용했었는데

react에서는 중괄호가 아닌 소괄호를 사용해야 해당 데이터를 받아들일 수 있다는 것을 알게 되었다.

```jsx
<div style={{display:'flex', justifyContent:'center',alignItems:'center'}}>
  {data.map((data)=> (<Datas data={data} />))}
</div>
```

그래서 버튼을 누르기 전에는 기존의 데이터 3개

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2015.png)

누르고 나서는

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2016.png)

---

`1219`

응용문제 

1. 버튼 2회 누를 때 
    
    [https://codingapple1.github.io/shop/data2.json](https://codingapple1.github.io/shop/data2.json) 에서
    
    [https://codingapple1.github.io/shop/data3.json](https://codingapple1.github.io/shop/data2.json) 으로 요청을 해서
    
    해당 데이터를 추가로 더 들고 오기
    
    (힌트: 버튼을 누른 횟수 체킹하기)
    
2. 버튼 3회 눌렀을 때는 상품이 더이상 없다고 알려주기
3. 버튼을 누를 때 AJAX 요청이 되기까지 “로딩중입니다” 문구를 띄우기
    
    ![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2017.png)
    

우선 내가 먼저 해결해야하는 부분은 

버튼을 클릭시 우측으로 계속 item이 생기는 것이 아니라

밑으로 row가 추가되도록 해야한다.

해결 방법

<Datas /> 컴포넌트를 감싸는 div 태그에 스타일 추가로

display를 grid 로 주어서 3개의 요소를 자동으로 공간차지하도록 하기 위해

1fr 1fr 1fr 이렇게 주어서 문제를 해결했다.

```jsx
<div style={{display:'grid', gridTemplateColumns:'1fr 1fr 1fr'}}>
  {data.map((data)=> (<Datas data={data} />))}
</div>
```

이후 해당 공간의 가운데로 정렬하기 위해 

해당 컴포넌트의 요소를 감사는 div 태그에 스타일 추가로

display:flex 를 추가하고 가운데 정렬을 했다.

```jsx
function Datas(props) {
  console.log(props);
  let dataId = props.data.id+1
  return (
    <div style={{display:'flex',justifyContent:'center',alignItems:'center'}}>
      <div style={{marginRight:'4px'}}>
        <img className='items' style={{height:'50%'}} src={'https://codingapple1.github.io/shop/shoes' + dataId +'.jpg'} alt="" />
        <p style={{marginTop:'7px'}}>{props.data.title}</p>
        <p>{props.data.content}</p>
        <p>{props.data.price}</p>
      </div>
    </div>
  )
}
```

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2018.png)

이제 응용문제 1번 해결하기

해결은 했는데 조금 찝찝한 부분이 있다

물론 사진이 없어서 어쩔 수는 없는 부분이지만;;

우선 해당 문제 버튼 2회 누를 때 해당 데이터를 추가로 더 들고 오기를 해결하기 위해서

힌트로 주셨던 버튼 누른 횟수를 state로 만들어 놓고 문제를 해결했다.

```jsx
let [btnClick,setBtnClick] = useState(0)
```

이후 기존의 axios 요청하는 주소에 해당 변수를 추가해주기 위해 코드를 작성했다.

```jsx
<div>
  <button onClick={()=> { 
    let urlNum = 2 + btnClick
    console.log(urlNum);
    axios.get('https://codingapple1.github.io/shop/data' + urlNum + '.json')
    .then((d)=> {
      console.log(btnClick);
      setBtnClick(btnClick+1)
      console.log(btnClick);
      let newData = [...data,...d.data]
      console.log(newData);
      setDatas(newData)
    })
    .catch((error)=> {console.log(error);})
  }}>버튼</button>
</div>
```

그런데 여기서 조금의 의아했던 부분이 

파이썬으로 치면 문자열 안에 변수를 넣기 위해선 f 스트링처럼 

JS에서는 중괄호를 작성후 작은 따옴표나 큰 따옴표를 작성해야 하는 줄 알았는데 

여기서는 아니었다.

분명 Detail.js 에서 img 를 받을때는 그렇게 했는데… (왔다갔다 하구마잉)

```jsx
<div style={{marginRight:'4px'}}>
  <img className='items' style={{height:'50%'}} src={'https://codingapple1.github.io/shop/shoes' + dataId +'.jpg'} alt="" />
  <div>
    <input onKeyDown={(e)=> {
      setInText(e.target.value);
    }} type="text" />
  </div>
  <p style={{marginTop:'7px'}}>{datas[data.id].title}</p>
  <p>{datas[data.id].content}</p>
</div>
```

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2019.png)

응용문제 2번 해결하기

버튼 3회 눌렀을 때는 상품이 더이상 없다고 알려주기

문제를 해결하는 방법은 굉장히 간단했다.

axios 요청이 실패했을 경우이기에 

.then () 부분이 아닌 .catch() 부분에 작성하면 되고

나는 alert() 를 이용해서 문구를 띄우는 방식으로 문제를 해결했다. 

(지금 베너의 정렬이 맞지 않는 건 나중에 수정할 예정)

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2020.png)

응용문제 3번 해결하기

버튼을 누를 때 AJAX 요청이 되기까지 “로딩중입니다” 문구를 띄우기

문제 해결 방법

나는 state를 활용해서 버튼 클릭시 

생성해둔 loding state를 true로 변경하고, axios 요청 성공시 false로 하여 

loding의 값이 true의 경우에만 Loding 컴포넌트를 보이도록하여 해결.

```jsx
let [loading,setLoading] = useState(false)

<div>
  <button onClick={()=> { 
    setLoading(true)
    let urlNum = 2 + btnClick
    console.log(urlNum);
    axios.get('https://codingapple1.github.io/shop/data' + urlNum + '.json')
    .then((d)=> {
      setLoading(false)
      setBtnClick(btnClick+1)
      let newData = [...data,...d.data]
      console.log(newData);
      setDatas(newData)
    })
    .catch((error)=> {
      alert('상품이 더이상 없습니다(❁´◡`❁)')
      console.log(error)
    })
  }}>버튼</button>
</div>

<div>
  {
    loading === true? <Loding /> : null
  }
</div>

function Loding() {
  return (
    <div style={{display:'flex',justifyContent:'center',alignItems:'center'}}>
      <img src="https://mblogthumb-phinf.pstatic.net/MjAyMDExMTJfMTgg/MDAxNjA1MTkxMjUwMzk4.BW7kx0zOQyxI57lwIxcYu40P1uicXhVNXQRSGegLuugg.RLMpOQkNfd72xWh8CJFLQz4ZwyGuZmWrDSdH8dfzArUg.GIF.bom____bom/90s_gif_(17).gif?type=w800" alt="" />
    </div>
  )
}
```

AJAX 추가 내용

서버로 데이터전송하는 POST 요청 할 경우

```jsx
axios.post('/주소', {name: 'kim'})
```

먄약 AJAX 요청을 여러개하려면?

```jsx
axios.get('url1')
axios.get('url2')
```

위와 같이 해도 되지만

아래와 같이 보통 작성한다  

단 아래의 경우 모두 성공할 경우 .then() 이렇게 적용된다.

```jsx
Promise.all([ axios.get('/url1'), axios.get('/url2'])
.then(()=> {})
```

그리고 원래 서버하고는 문자만 주고받을 수 있다고한다.

물론 array, object 또한 주고 받을 수 있는데 

```jsx
"{"name":"kim"}" 이렇게 문자이어야 주고 받을 수 있다.

// 위와 같은 형식을 JSON 이라고 한다.
// 그래서 axios가 자동으로 array 형식으로 바꿔주기 때문에 받아올 수 있다.
```

외부 라이브러리인 axios 가 아닌 fetch() 를 사용할 경우 JSON 형식으로 데이터를 받아오기에 

array 또는 object로 변환하는 과정이 필요하다.

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2021.png)

리엑트에서 탭 UI 만들기

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2022.png)

순서 

1. Html CSS로 미리 디자인
    
    ```jsx
    <Nav variant="tabs" defaultActiveKey="link0">
            <Nav.Item>
              <Nav.Link eventKey="link0">버튼0</Nav.Link>
            </Nav.Item>
            <Nav.Item>
              <Nav.Link eventKey="link1">버튼1</Nav.Link>
            </Nav.Item>
            <Nav.Item>
              <Nav.Link eventKey="link2">버튼2</Nav.Link>
            </Nav.Item>
          </Nav>
          <div>내용0</div>
          <div>내용1</div>
          <div>내용2</div>
    ```
    
2. 탭 상태 저장해둘 state 필요
    
    ```jsx
    let [탭, 탭변경] = useState(0)
    ```
    
3. state에 따라서 UI가 어떻게 보일지 작성

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2023.png)

삼항 연산자를 사용하여 문제를 해결한다면

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2024.png)

위의 사진과 같이 여러개의 삼항 연산자를 사용해야하기에 비효율적이다.

그래서 일반 if 조건문을 사용하여 해결하기

리엑트에서 일반 조건문을 html 내에서 사용할 수 없기 때문에  function 바깥에 작성을 해야한다.

```jsx
if (탭 === 0) {
  <div>내용</div>
} else if (탭 === 1) {
  <div>내용1</div>
} else if (탭 === 2) {
  <div>내용2</div>
}
```

그래서 조건문을 작성하고 난 뒤 Html에 해당 내용을 넣으려고 할 경우 

function 컴포넌트를 작성해서 html 안에 넣어주기

```jsx
function TabContent() {
  if (탭 === 0) {
    <div>내용</div>
  } else if (탭 === 1) {
    <div>내용1</div>
  } else if (탭 === 2) {
    <div>내용2</div>
  }
}
```

그리고 컴포넌트를 return 문이 없으면 안되기 때문에 return 추가해주기

```jsx
function TabContent() {
  if (탭 === 0) {
    return <div>내용</div>
  } else if (탭 === 1) {
    return <div>내용1</div>
  } else if (탭 === 2) {
    return <div>내용2</div>
  }
}
```

Q. 버튼 1 누르면 내용 1 보이게 하기

```jsx
<div style={{display:'flex', justifyContent:'center',alignItems:'center'}}>
  <Nav variant="tabs" defaultActiveKey="link0">
    <Nav.Item>
      <Nav.Link onClick={()=> {탭변경(0)}} eventKey="link0">버튼0</Nav.Link>
    </Nav.Item>
    <Nav.Item>
      <Nav.Link onClick={()=> {탭변경(1)}} eventKey="link1">버튼1</Nav.Link>
    </Nav.Item>
    <Nav.Item>
      <Nav.Link onClick={()=> {탭변경(2)}} eventKey="link2">버튼2</Nav.Link>
    </Nav.Item>
  </Nav>
</div>

function TabContent(porps) {
  if (porps.탭 === 0) {
    return <div>내용</div>
  } else if (porps.탭 === 1) {
    return <div>내용1</div>
  } else if (porps.탭 === 2) {
    return <div>내용2</div>
  }
}
```

팁

1.  props.어쩌구가 귀찮을 경우 {} 중괄호에 변수 작성 (여러개도 가능)
    
    ```jsx
    function TabContent({탭}) {
      if (탭 === 0) {
        return <div>내용</div>
      } else if (탭 === 1) {
        return <div>내용1</div>
      } else if (탭 === 2) {
        return <div>내용2</div>
      }
    }
    ```
    
2. 조건문 없이 작성해 볼 수도 있다.
    
    ```jsx
    function TabContent({탭}) {
    	return [<div>내용</div>,<div>내용1</div>,<div>내용2</div>][탭]
    }
    ```
    
3. 여기서 하나의 태그를 return 문으로 넘겨주려 할 경우 
 안에 내용은 중괄호로 감싸줘야하는 것 같다.
    
    ```jsx
    function TabContent({탭}) {
      return (
        <div>
          { [<div>내용</div>,<div>내용1</div>,<div>내용2</div>][탭] }
        </div>
      )
    }
    ```
    

---

`1220`

전환 애니메이션 주기 (Transtiton)

전환 애니메이션은 부착하면 애니메이션 되는 className 하나 만들고 원할 떄 부착하여 사용해보기

순서

1. 애니메이션 동작 전 className 만들기
    
    ```css
    .start {
    	opacity: 0;
    }
    ```
    
2. 애니메이션 동작 후 className 만들기
    
    ```css
    .end {
    	opacity: 1;
    	transition: opacity 0.5s;
    }
    ```
    
3. className에 transition 속성 추가
    
    ```jsx
    function TabContent({탭}) {
      return (
        <div className='start end'>
          { [<div>내용</div>,<div>내용1</div>,<div>내용2</div>][탭] }
        </div>
      )
    }
    ```
    
4. 원할 때 2번 className 부착
    1. 우선 우리는 3개의 버튼이 있는데 각각의 [Nav.Link](http://Nav.Link) 마다 작성하게 되면
     코드가 너무 많아지니까 탭 state가 변할 때 end 클래스를 부착하도록 해보기
        1. state가 변할 때 마다라는 이야기가 나오게 되면 useEffect() 를 사용하기!! 
            
            ```jsx
            useEffect(()=> {
            	
            }, [])
            
            ```
            
        2. start 클래스가 있는 태그를 선택해야하기에 바닐라 JS 를 사용해도 되지만
         React적으로 사용한다면 state를 생성해보기 
            
            ```jsx
            let [fade, setFade] = useState('')
            ```
            
        3. 이후 useEffect를 통해 fade를 end 로 바꿔달라고 하기
            
            ```jsx
            useEffect(()=> {
            	setFade('end')
            }, [탭])
            ```
            
        4. 이후 문자 중간에 변수를 넣어야 하기에 중괄호 이후 + 를 사용해서 추가해주기
            
             여기서 +를 사용하지 않는다면 에러가 발생한다.
            
             또 중요한 부분이 클래스에서는 띄어쓰기를 기준으로 추가가 되기에 
             start 하고 한칸을 띄워줘야 한다.
            
            ```jsx
            <div className={'start '+ fade}>
            
            </div>
            ```
            
            또는 백틱 `` 을 넣어서 $와 함께 사용해줘도 가능하다
            
            ```jsx
            <div className={`start ${fade}`}>
            
            </div>
            ```
            
        5. 실행해보면 아직 안된다 이유는 
         클릭하게 되면 부착은 되는데 다른 탭을 누를 때마다 때어냈다가
         부착을 해야 효과가 보이기 때문.
            
            
            ```
            function TabContent({탭}) {
              let [fade,setFade] = useState('')
            
              useEffect(()=> {
            		setFade('')
                setFade('end')
              }, [탭])
            
              return (
                <div className={'start '+ fade}>
                  { [<div>내용</div>,<div>내용1</div>,<div>내용2</div>][탭] }
                </div>
              )
            }
            ```
            
             setFade() 를 그냥 추가 해봤지만 실행이 되지 않는다
            
        6. 그래서 useEffect()의 clean up function을 사용하는 것
            
            ```jsx
            function TabContent({탭}) {
              let [fade,setFade] = useState('')
            
              useEffect(()=> {
                setFade('end')
                return ()=> {
                  setFade('')
                }
              }, [탭])
            
              return (
                <div className={'start '+ fade}>
                  { [<div>내용</div>,<div>내용1</div>,<div>내용2</div>][탭] }
                </div>
              )
            }
            ```
            
            다만 이렇게 해도 의도한 대로 작동하지는 않는다.
            
            그래서 결과적으로 해결하는 방법은 end를 부착하는 시점을 뒤로 미뤄주면 된다.
            
            시간을 두고 행동을 하는 것이기에 타이머를 이용하면 된다고 생각하면 된다.
            
            ```jsx
            function TabContent({탭}) {
              let [fade,setFade] = useState('')
              useEffect(()=> {
                setTimeout(() => {
                  setFade('end')
                }, 300);
                return ()=> {
                  setFade('')
                }
              }, [탭])
            
              return (
                <div className={'start '+ fade}>
                  { [<div>내용</div>,<div>내용1</div>,<div>내용2</div>][탭] }
                </div>
              )
            }
            ```
            
            이유를 설명하기전에 리엑트 18버전 이후로 나온 기능 중에
            
            automatic batching 기능이라는 것이 나왔다고 한다.
            
            의미는 state 변경 함수들이 근처에 있다고 한다면 
            
            합쳐서 하나의 함수만 실행시키도록 하는 기능이라고 한다.
            
            즉 state변경 함수를 사용할때마다 재렌더링을 하는 것이 아니라 
            
            state가 변경되는 마지막 한번만 재렌더링을 시켜준다고 한다.
            
            그래서 위에 작성한대로
            
            ```jsx
            function TabContent({탭}) {
              let [fade,setFade] = useState('')
            
              useEffect(()=> {
                setFade('end')
                return ()=> {
                  setFade('')
                }
              }, [탭])
            
            // -------------------------------------------------------
            
            function TabContent({탭}) {
              let [fade,setFade] = useState('')
            
              useEffect(()=> {
            		setFade('')
                setFade('end')
              }, [탭])
            
            // 두 개의 방법 모두 의도대로 실행 되지 않는다는 점
            
            ```
            
            ![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2025.png)
            
            2빠가 마지막이기에 1빠의 함수로는 재렌더링이 되지 않는다는 점
            
            그리고 타이머를 넣어줬기에 이때 계속해서 새로고침을 하게 되면 
            
            타이머가 계속해서 늘어나게 되기에 타이머를 클리어해줘야 하기에
            
            ```jsx
            function TabContent({탭}) {
            
              let [fade,setFade] = useState('')
            
              useEffect(()=> {
                let a = setTimeout(() => {
                  setFade('end')
                }, 300);
            
                return ()=> {
            			clearTimeout(a)
                  setFade('')
                }
              }, [탭])
            
              return (
                <div className={'start '+ fade}>
                  { [<div>내용</div>,<div>내용1</div>,<div>내용2</div>][탭] }
                </div>
              )
            }
            ```
            
            그리고 css 요소로 크기가 점점 커지게 하는 효과를 주고자한다면
            
            transform: scals() 을 주면 된다.
            
            숙제 
            
            Detail 페이지 로드시 
            
            투명도 0 → 1 애니메이션을 주고 싶다면??
            
            위에서 작성한 것처럼
            
            1. useState 변수를 생성 후 
                
                ```jsx
                let [fade, setFade] = useState('')
                ```
                
            2. mount 시에 실행 시키도록 useEffect() 를 작성
                
                ```jsx
                useEffect(()=> {
                
                }, []) 
                ```
                
            3. 타이머를 사용하여 automatic batching 효과를 적용되지 않도록 하기
                
                ```jsx
                useEffect(()=> {
                	let a = setTimeout(()=> {setFade('end')},250)
                }, []) 
                ```
                
            4. clean up function을 사용해주기
                
                ```jsx
                useEffect(()=> {
                	let a = setTimeout(()=> {setFade('end')},250)
                	
                	return ()=> { 
                		clearTimeout(a)
                		setFade('')
                	}
                }, []) 
                ```
                
            5. 적용되는 태그에 state 를 문자로 추가해주기
                
                ```jsx
                <div className={"start" + fade}>
                ```
                
        
        Context API 사용해보기
        
        - Single Page Application 단점:
            - 컴포넌트간의 state 공유가 어렵다는 점
            
            ![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2026.png)
            
            - 단 부모 → 자식 관계의 경우 props로 전송은 가능하다
        
        - 우선 현재 컴포넌트 상황
            - shoes 라는 state를 TabContent 컴포넌트에서 사용하려면 
            props 를 2번이나 해야하기에 번거롭다.
            
            ![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2027.png)
            
            ![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2028.png)
            

그래서 props를 하지 않아도 되는 2가지 방법이 있다.

1. Context API (리액트 기본문법)
    1. props 전송없이도 state 공유 가능
    2. 단 잘 사용하지는 않는다
        1. 성능 이슈
        2. 컴포넌트 재활용이 어렵다.
2. Redux 등 외부라이브러리 사용 (Vue때 사용했었음)

Context API는 우선 간단하게 이런게 있다는 정도로만 이해하기 

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2029.png)

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2030.png)

Context API setting 순서는 총 3가지가 있다.

1. (context 를 만든다는 것으로 state 보관함이라는 의미)
    
    ```jsx
    import { createContext, useState } from "react"
    
    let Context1 = createContext()
    ```
    
2. <Context.Provider> 로 원하는 컴포넌트 감싸기
    
    ```jsx
    <Route path='/detail/:id'  element={
    	<Context1.Provider>
    		<Detail datas={datas}/>
    	</Context1.Provider>
    }/>
    ```
    
3. 공유를 원하는 state를 value={{ }} 에 담아서 보내주기
    
    ```jsx
    <Route path='/detail/:id'  element={
    	<Context1.Provider value={{ state1, state2 }}>
    		<Detail datas={datas}/>
    	</Context1.Provider>
    }/>
    ```
    

이렇게 위와 같이 작성을 한다면 

해당 컴포넌트 안의 모든 컴포넌트는 value 안의 모든 state를 사용할 수 있게 된다.

해당 컴포넌트 안에서의 state 사용하는 순서

1. Context를 import 해오기
 기존에 App.js 에서 정의했던 Context1 을 그냥 정의하는 것이 아니라 export 를 함께 해주기
    
    ```jsx
    // App.js
    export let Context1 = createContext()
    
    // 사용할 컴포넌트 지금 경우엔 Detail.js
    import {Context1} from './App.js' <- 경로
    ```
    
2. useContext(Context) 작성하기
 useContext() 의 역할은 보관함인 Context를 해체해주는 역할
    
    ```jsx
    // Detail.js
    import { useContext, useEffect, useState } from 'react'
    
    function Detail(props) {
    	
    	useContext(Context1)
    }
    ```
    

그래서 useContext() 로 해체한 데이터를 변수에 담아서 사용을 할텐데

```jsx
// 아래와 같이도 가능하지만
let a = useContext(Context1)

// 데이터를 좀 더 편하게 가져다 사용하기 위해 Destructuring 을 한다면
let {state1, state2} = useContext(Context1)
```

사용할때는 중괄호 {} 에 담아서 사용하면 됨.

```jsx
{ state1 }
```

이렇게 Detail 컴포넌트에서도 사용이 가능하지만 

더욱 편한 점은 하위의 모든 컴포넌트들도 사용이 가능하기 때문에 

하위 컴포넌트에서는 아래의 코드만 작성해주면 사용이 가능하다.

```jsx
let {state1, state2 } = useContext(Context1)
```

여기서 Context API를 사용하지 않는 특징

1. state 변경시 쓸데없는 것까지 재렌더링 한다는 점

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2031.png)

1. 나중에 컴포넌트 재사요이 어려움

![Untitled](React%202%2027854ff5e22040be9c442f036dd89914/Untitled%2032.png)