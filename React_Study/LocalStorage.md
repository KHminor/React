# LocalStorage

`1224`

LocalStorage로 만드는 최근 본 상품 기능

원래 새로고침을 하게되면 state는 초기 값으로 돌아가게 되는데

그게 싫다면 서버로 보내서 DB에 영구 저장하면 된다.

만약 나는 서버도 DB도 모르겠다 라면 

차선책으로 LocalStorage를 사용하는 방법이 있다. (데이터를 반영구적으로 저장가능)

LocalStorage 확인하는 방법

- 개발자도구에서 Application탭의 Storage의 Local Storage 클릭
    - 브라우저에서 제공하는 데이터 저장소

Local Storage의 특징

1. key: value 형태로 저장가능하다.
    
     
    
    ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled.png)
    
    ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%201.png)
    
2. 최대 5MB까지 문자만 저장 가능하다
3. 사이트를 재 접속해도 남아있다. (브라우저 청소하면 삭제됨)

Local Storage와 Session Storage의 차이

- Local Storage는 재 접속해도 남아있지만
- Session Storage는 브라우저를 끄면 날라간다는 차이점이 있다.

Lcal Storage에 데이터를 넣는 방법

- console창에 해도 된다.
- 데이터를 저장 하는 방법
    - localStorage.setItem( ’ 이름 ’, ‘ 값 ‘ )
    
    ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%202.png)
    
    undefined 문구가 나와야 잘 저장이 된것
    
    ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%203.png)
    
- 데이터를 출력하는 방법
    - localStorage.getItem(’key’)
    
    ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%204.png)
    
    - 그리고 숫자를 입력해도 문자가 출력 되는 것을 볼 수 있다.
    
    ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%205.png)
    
- 데이터를 삭제하는 방법
    - localStorage.removeItem(’key’)
    
    ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%206.png)
    
- 데이터를 수정하는 방법
    - 따로 데이터를 수정하는 문법은 없다.
    - 그래서 데이터를 꺼내서 수정하고 집어넣으면 된다고 한다.
    
    ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%207.png)
    
    이렇게 하면 되지 않을까??
    
- 그리고 sessionStorage에 데이터를 넣고 싶다면 
 localStorage 대신 sessionStorage를 작성해주고 뒤에는 똑같이 작성해주면 된다.
- 또 array 또는 object 를 localStorage 또는 sessionStorage에 저장하고자 할 경우
    - 원래는 문자만 저장이 가능하기에 저장이 안되지만
    - 편법을 사용하여 JSON 형태로 변경한다면 저장이 가능하다
    - 일반적으로 생각했을 때 넣는 방법(object가 깨지는 방법)
        
        ```jsx
        // App.js
        let obj = {name: 'kim'}
          localStorage.setItem('data', obj)
        ```
        
        위와 같이 작성 후 확인을 해본다면 아래 사진과 같이 object 값이 깨지게 된다.
        
        ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%208.png)
        
        그래서 JSON 형태로 값을 변경하여 넣어줘야 한다.
        
        해결 방법
        
        - array 또는 obejct 를 담은 변수를 JSON.stringify() 메서드 안에 넣어주어
         JSON 형태로 변환해주기
            
            ```jsx
            // local Storage에 array 또는 object 저장해보기 (JSON 형태)
              let obj = {name: 'kim'}
              localStorage.setItem('data', JSON.stringify(obj))
            ```
            
            ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%209.png)
            
        - 저장한 데이터를 꺼내는 방법
            
            ```jsx
            //저장된 데이터를 꺼내보기
              let d = localStorage.getItem('data')
              console.log(d);
            ```
            
            ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%2010.png)
            
            위의 사진과 같이 JSON 형태로 따옴표가 붙여져서 나오게 된다.
            
            그래서 [d.name](http://d.name) 과 같이 object형태로 데이터를 가져올 수 가 없게 되어서
             JSON 데이터를 array 또는 object 형태로 변환해줘야 한다.
            
            변환해주는 방법
            
            - JSON.parse() 메서드를 사용해서 변환해주기
                
                ```jsx
                // 저장된 데이터를 JSON-> array/object로 변환 후 출력
                  console.log(JSON.parse(d));
                  console.log(JSON.parse(d).name);
                ```
                
            
            ![Untitled](LocalStorage%2015b9306ff1f94165af6c1da66cb2c0e9/Untitled%2011.png)
            
            과제
            
            - 최근 본 상품(디테일 페이지로 들어가서 본 상품)을 메인 페이지에 나열하기
                - localStorage 데이터의 key값은 watched, value 값은 array로 저장하기
                - 그런데 기대치가 낮다고 그냥
                    1. localStorage 에 해당 상품의 id값만 넣어주기
                        - 단! 번호 중복은 막기
                    2. localStorage 의 초기값은 App.js가 mount 되었을 때 
                     useEffect를 활용해 리스트 값으로 초기화 해주기
                    
                    ```jsx
                    useEffect(()=> {
                    	localStorage.set('watched',JSON.stringify([]))
                    },[])
                    ```
                    
    
    과제 해결
    
    - 흠… 정말 어렵게 생각해버렸다.
        - 처음엔 store에 localStorage 데이터를 보관하며 해당 데이터를 localStorage에 넣는
         그런 좀 꼬아서 생각해버렸는데 … 그렇게 하지 않아도 괜찮았다…
    
    - 해결 방법
        
        useEffect 사용
        
        1. App.js
            1. 메인 페이지에 들어오게 되면 마운트시 localStorage에 watched 데이터를 만들기
            
            ```jsx
            // App.js
            
            useEffect(()=> {
            	localStorage.setItem('watched',JSON.stringify([]))
            },[])
            ```
            
        2. Detail.js
            1. 디테일 페이지에 들어오게 되면 마운트시 현재 페이지에 있는 상품의 id 값을 
             localStorage에 추가 하기
        
        ```jsx
        useEffect(()=> {
        	let watchedData = localStorage.getItem('watched')
        	watchedData.JSON.parse(watchedData)
        	// 데이터 추가
        	watchedData.push(data.id)
        	// 중복 제거
        	watchedData = new Set(watchedData)
        	// Array로 타입 변경
        	watchedData = Array.from(watchedData)
        	// 데이터 새로 추가
        	localStorage.setItem('watched',JSON.stringify(watchedData))
        },[])
        ```
        
- 응용 문제
    - 현재 새로고침시 초기값으로 돌아가게 되는데 
    만약 이미 watched에 데이터가 있다면 setItem 하지 말아달라고 하는 방법은?
- 해결 방법
    - App.js
        - 해당 페이지의 요소들이 마운트 되었을 때 localStorage의 watched 값이 없다면
         초기값으로 빈 리스트를 추가하도록 코드를 짜기
        
        ```jsx
        useEffect(()=> {
            let checkLocal = localStorage.getItem('watched')
            if (!(JSON.parse(checkLocal))) {
              localStorage.setItem('watched',JSON.stringify([]))  
            }
          },[])
        ```
        
- 그리고 모든 state를 localStorage에 자동저장 하고 싶다면 
 redux-persist 외부 라이브러리를 사용하면 된다고 한다.
- 또한 Redux를 state 관리 라이브러리라고 하는데
    - 다른 state 관리 라이브러리도 많다고 한다.
        - Jotai
        - Zustand