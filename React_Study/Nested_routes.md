# Nested routes

`2023-01-23`

nested routes는 예를 들어

```tsx
<Route path="/about" element={<About />}/>
<Route path="/about/member" element={<About />}/>
<Route path="/about/location" element={<About />}/>
```

위와 같이 about 라우트에 member, location 이렇게 두 개를 만들어주려 할 때

반복해서 about을 넣어줄 필요 없이

아래와 같이 Route를 닫는 태그를 넣어 추가해주고 중복되는 route는 제거해주면 된다.

```tsx
<Route path="/about" element={<About/>}>
  <Route path="member" element={<About/>}/>
  <Route path="location" element={<About/>}/>
</Route>
```

nested route의 장점

1. route 작성이 더욱 간단해진다.
2. nested route 접속 시 element가 위의 경우엔 두 개나 보이게 된다.
    1. 단 위와 같이 작성할 시엔 보이지 않게 되고 어디에 보여줄지 작성해야 한다.
    2. 어디에 보여줄지는 Outlet이라는 route 라이브러리에서 import해서 
     컴포넌트 형식으로 상위 Route에 작성해주면 된다.
    
    ```tsx
    // About component
    
    function About(){
    	return (
    		<div>
    			<h4>어바웃 페이지임</h4>
    			<Outlet></Outlet>
    		</div>
    	)
    }
    
    ```
    
- 그래서 Outlet은
    - nested routes의 element 를 보여주는 곳을 의미한다.
- 그리고 nested routes는
    - 여러 유사한 페이지가 필요할 경우 사용