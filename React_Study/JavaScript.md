# JavaScript

`1130`

## JS(한번 더 정리해보기)

웹환경에서 JavaScript의 목적

=  HTML 조작과 변경

### 처음 배울 거: HTML 조작

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled.png)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%201.png)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%202.png)

위의 사진과 같이도 가능

### UI 만드는 법:

1. 미리 디자인해놓고 숨김
2. 버튼 누르거나 하면 보여줌

css 연결 

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%203.png)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%204.png)

과제:

만약 아래와 같은 코드가 주어졌을 때 버튼을 눌렀을 때만 보이도록 하기 위한 JS 작성

```jsx
// JS
<div class="alert-box">Alert 박스</div>
```

```css
// css
.alert-box {
  background-color: #aba8f4;
  color: #4646b4;
  padding: 20px;
  border-radius: 5px;
  display: none;
}
```

실습:

```jsx
<div id='alert' class='alert-box'>Alert 박스</div>
<button onclick='document.getElementById('alert').style.display="block" '>❤</button>
```

### function 문법 사용하기

긴 코드를 깔끔하게 한 단어로 축약가능

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="main.css" />
  </head>
  <body>
    <div id="alert" class="alert-box">
      Alert 박스
      <button onclick="알림창닫기()">💔</button>
    </div>
    <button onclick="알림창열기()">❤</button>

    <script>
      function 알림창열기() {
        document.getElementById("alert").style.display = "block";
      }
      function 알림창닫기() {
        document.getElementById("alert").style.display = "none";
      }
    </script>
  </body>
</html>
```

function을 적용 할 경우 () 소괄호를 함께 넣어줘야 작동한다.

에러메세지

1. console에 of null 이라는 문구가 있다면 왼쪽에 값이 텅 비어있다라는 의미
2. is not a function 이라는 문구가 있다면 대소문자 또는 오타로 인한 에러메세지

function 2

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%205.png)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%206.png)

위와 같이 인자값을 사용하는 이유

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%207.png)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%208.png)

위와 같이 함수를 정의 한다면

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="main.css" />
  </head>
  <body>
    <div id="alert" class="alert-box">
      Alert 박스
      <button onclick="알림창('block')">💔</button>
    </div>
    <button onclick="알림창('none')">❤</button>

    <script>
      function 알림창(구멍) {
        document.getElementById("alert").style.display = 구멍;
      }
    </script>
  </body>
</html>
```

### addEventListener

그전에 getElementByClassName은 ( ‘클래스명’ )을 작성하면 클래스가 적힌 모든 태그를 조회 후 

해당 리스트의 몇번째에 접근 할 수 있도록 [0] 을 작성하면 된다. 

```jsx
function 알림창() {
	document.getElementByClassName('클래스명')[선택할 리스트 번호 ]
}
```

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%209.png)

### jQuery

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2010.png)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2011.png)

jquery cdn을 가져와서 설치하기 —> body 내부의 하단에 작성 

기존의 javascript 문법을 jQuery로 변경시 (근데 react 가 나온 뒤 react가 최고)

```jsx
// javascript
document.getElementById('test').innerHTML = '안녕';

// jQuery
$(#'test').html('안녕')  

//간.단
```

```jsx
// CSS 같은 경우

$('#test).CSS('color','red')
```

```jsx
// 속성 추가 or 변경
$('test').attr('src','~~~~~')

```

---

---

`1211`

1. ‘1’ + 1 = ‘11’ 이렇게 
문자 1과 숫자 1을 더하게 되면 문자 11이 출력된다.
2. 문자열 안에 따옴표를 사용하려 할 경우
    1. ex. ‘여기는 문자열 ‘작은’따옴표’
    2. 위와 같은 경우 작은 따옴표 안에 작은 따옴표가 있기에 에러가 뜨게 된다. 
    3. 해결 방법은
    4. ex. ‘여기는 문자열 \‘작은\’따옴표’
    5. 이스케이프 표현을 사용하여 다음 작은 따옴표는 문자 그대로 사용할 것임을 표시 
    
    ![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2012.png)
    
3. 백틱을 사용해서 출력하고자 할 경우
    
    ```jsx
    const Name = '홍길동'
    let age = 20
    let married = false
    
    console.log(
    `제 이름은  + Name + , 나이는  + age + 세구요, 
    + $(married ? '기혼' : '미혼') + 입니다`)
    ```
    
4. 비교
    1. x ===y
    2. x !==y
    
    비교 연산자는 사전순 상 먼저 나오는게 작은 값으로 적용
    
    ex.
    
    1. ‘100’ > ‘12’ 
        1. false
        2. 문자는 사전 순으로 비교
    2. 100 > 12
        1. true
    3. ‘100’ > 12
        1. true
        2. 문자와 숫자를 비교하면 문자를 숫자로 변환
    
    4. 문자열 값에 숫자, null, undefined 를 넣게 되어도 다 문자로 변경 된다.
    
    ```jsx
    let a = 'hello'
    a += 1
    a += null
    a += undefined
    console.log(a)
    // hello1nullundefined
    ```
    
    1. JS에서 정수, 소수, 음수인 소수 모두 타입이 number로 찍힌다.
    2. JS에서 1/0은 Infinity가 나온다. 물론 타입은 number
    원래 다른 언어에서는 에러가 뜨는데 말이지…
        
        ![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2013.png)
        
        1. 그래서 해당 Infinity 값에 +1을 하더라도 결과값은 Infinity가 나온다. 
        2. 또한 Infinity에도 음수(-Infinity)와 양수(Infinity)가 있다.  
        3. 또한 Infinity는 바로 변수에 넣을 수 있는 예약어이다.
    3. NaN
        
        ```jsx
        let x = 1/'abc'
        let y = 2 * '가나다'
        let z = NaN
        // 모두 NaN 이 나오면서 타입은 number
        ```
        
        ![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2014.png)
        
        마찬가지로 NaN에 어떠한 값을 넣어도 NaN이다.
        
        그리고 NaN은 Infinity와는 다르게 양수 음수가 없다.
        
        그리고 NaN인지 아닌지 확인하는 방법은 두가지가 있다.
        
        ```jsx
        let x = NaN
        console.log(
        	x, // false
        	x == NaN, // false
        	x === NaN, // false
        	isNaN(x), // true
        	Number.isNaN(x) // true
        )
        ```
        
    4. 숫자
        
        ![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2015.png)
        
        ![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2016.png)
        

---

`1215`

부정 연산자

- true, !true, false, !false
- !( 1 == ‘1’), !( 1 === ‘1’)

AND/OR

- AND : 앞의 것이 false 면 뒤의 것을 평가할 필요 없음
    - &&
- OR : 앞의 것이 true 면 뒤의 것을 평가할 필요 없다.
    - ||

```jsx
let x = 14;

console.log(
	( x > 10 && x <= 20) || x % 3 === 0
); 

// true
```

요롷게 해당 변수에 값을 넣기도 가능하네??

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2017.png)

삼항연산자

```jsx
let x = true;

let y = x ? '참입니다' : '거짓입니다';

console.log(y) // 참입니다.
```

이것도 좀 신기한듯;;

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2018.png)

- 소수이어도
- 음수이어도
- 문자 0 이어도
- 띄워쓰기가 있는 문자이어도
- 양/음 무한대이어도
- 빈 객체이어도
- 모두 true

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2019.png)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2020.png)

이것도 위에서 말했지만 조건으로 인해 뒤에까지 갔을 때 문자열이 있을 경우 
해당 문자를 변수에 넣게 된다.

쉼표 연산자

아래와 같이 변수를 한번에 선언할 수 있다.

```jsx
let x = 1, y = 2, z = 3
```

또한 console.log() 안에 쉽표가 여러개 있다면 가장 마지막 것을 반환한다.

```jsx
console.log(
	(++x, y+= x, z *= y)
)
```

null 병합 연산자 - ??

- || 와 달리, falsy가 아닌 해당 값이 null 또는 undefined 이면 다음 조건으로 향하기

```jsx
let x;
x ?? console.warn(x, 'x에 값이 없습니다'); // undefined x에 값이 없습니다

x = 0
x ?? console.warn(x, 'x에 값이 없습니다'); // error

x = null
x ?? console.warn(x, 'x에 값이 없습니다'); // null x에 값이 없습니다
```

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2021.png)

And, Or, ?? 도 할당 연산자가 가능

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2022.png)

연산자 우선순위

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2023.png)

---

`1216` 

객체와 배열 알아보기

객체(Object) 

- JS 에서 원시 타입이 아닌 모든 데이터는 근본적으로 객체이다.
- 복합적인 정보를 Property (프로퍼티) 라고 하는 키와 값의 조합으로 저장하는 자료형

```jsx
const person1= {
	name: '김철수',
	age: 25,
	married: false
}
```

프로퍼티 접근

```jsx
// 두가지 방법 모두 가능하다
// 단 대괄호로 조회를 할 경우엔 내부 key 값을 문자열로 만들어줘야한다.

console.log(
	person1.name,
	person1.age,
	person1.married
)

console.log(
	person1["name"],
	person1["age"],
	person1["married"]
)
```

그리고 없는 key에 대한 값을 가져오려 할 경우 

JS에선 undefined 가 나오게 되며 error 는 발생하지 않는다.

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2024.png)

또한 객체안에 해당 key 값이 존재하는지에 대한 것도 알 수 있다.

```jsx
console.log(
	'age' in person1,
	'job' in person1
}
```

프로퍼티 수정 및 추가

```jsx
// 특정 프로퍼티의 값 변경
person1.age = 30
person1['married'] = true

// 새 프로퍼티 추가
person1.job = 'developer'
person1['bloodtype'] = 'AB'

// 신기한 점인것이 person1은 const(상수) 임에도 내용은 수정할 수 있다는 것.
// 이유는 할당 되어있는 객체 안에 새로운 값을 넣는 것은 가능하지만
// 아예 다른 값 차제를 담아버리게 되면 error가 생기게 된다.
```

배열(Array)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2025.png)

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2026.png)

배열 또한 객체와 같이 해당 리스트를 열어보면 

key인 index 값과 value 값이 함께 담겨져 있다는 것을 알 수 있다.

Object과 다른 점은 

Object는 Obj.key 가 가능하지만

Array에서는 대괄호의 접근만 가능하다.

다만 Array.length는 가능하다.

값을 얻는 방법과 길이에 대한 접근

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2027.png)

 

Array의 가장 마지막 요소 접근하는 방법은

Array[Array.length -1]

Array값 수정 및 추가

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2028.png)

Object와 마찬가지로 const인 상수 타입이어도 해당 객체 안의 내용을 수정 및 추가하는 것은

가능하며 해당 Array 자체를 변경하게 되면 error가 생기게 된다.

그리고 Array 길이가 넘어가는 값에 접근하려고 할 경우 Object와 마찬가지로 undefined가 뜬다.

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2029.png)

그리고 Object와 Array는 서로 번갈아가며 사용이 가능하다.

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2030.png)

전역 스코프와 블록 스코프 

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2031.png)

전역변수를 많이 사용하게 되면 그만큼 프로그램을 실행 시키는 동안 계속 

메모리 공간을 차지 하기 때문에 지양해야한다.

조건문

If 문

```jsx
const open = true

// 한줄 코드
if (open) console.log('영업중입니다.')
// 영업중입니다.

// 여러줄 코드 - 블록문 사용
if (open) {
	console.log('환영합니다.')
	console.log('즐거운 쇼핑하세요!')
}

// 환영합니다.
// 즐거운 쇼핑하세요!

// if ~ else 문

const x = 20;

if (x % 2) {
	console.log('홀수입니다')
} else {
	console.log('짝수입니다')
}

// 짝수입니다
```

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2032.png)

switch

특정 값에 대한 다수의 옵션이 있을 때 사용 (if문 중복으로 사용하는 것 보단 가독성이 좋다고 함)

```jsx
const fingerOut = 2;

switch (fingerOut) {
	
	// 순서 상관 없음
	case 2:
		console.log('가위');
		break;
	case 0:
		console.log('바위')
		break;
	case 5:
		console.log('보')
		break;
	default:
		console.log('무효')
}
```

만약 break가 없다면 해당 지점부터 default 까지 수행하게 된다.

default는 해당 case 값과 맞지 않는 경우에 수행하게 된다.

객체를 사용한 방법

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2033.png)

여러개의 케이스를 사용한 switch문

case는 break가 없으면 계속 수행되는 것을 활용한 문법

![Untitled](JavaScript%2010901ecf8b684e6c84cad7d3ae1e453e/Untitled%2034.png)

---

for 루프