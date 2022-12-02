[리액트를 다루는 기술]

2장 
=============

리액트는 뷰만 신경쓰는 라이브러리라고 할 있음 
프레임 워크는 Ajax, 데이터 모델링, 라우팅 등의 기능을 내장하고 있음

yarn은 npm을 대체 할 수 있는 도구로 npm보다 빠르며 효율적인 캐시 시스템과 기타 부가기능을 제공 하고 있음

* 리액트에서 조건문(if)사용하기
JSX 내부의 자바스크립트 표현식에서 if문을 사용할 수 없지만 {} 안에 조건부 연산자, 즉 삼항 연산자를 사용할 수 있음

- 특정 조건을 만족할 때 내용을 보여주고 아닐 때 아예 아무것도 렌더링 하지 않아야 할 경우
```js
{name === 'react' && <h1>react!</h1> : null}
```
- 위의 경우를 &&(AND)를 사용하여 더 짧게 표현 
```js
{name === 'react' && <h1>react</h1>
```
falsy한 값인 0은 예외적으로 화면에 나타남

- undefined를 렌더링하지 않기   
리액트 컴포넌트에서는 함수에서 undefined만 반환하여 렌더링하는 상황을 만들면 안됨   
||(OR)연산자를 사용하면 해당 값이 undefiend일때 사용할 값을 지정할 수 있어 오류 방지 할 수 있음   

```js
const name = undefined;
return name || '값이 undefined입니다.';
```

- name 값이 undefined일때 보여 주고 싶은 문구가 있다면 

```js
const name = undefined;
return <div> {name || '보여 주고 싶은 문구내용'}</div>;
```

* Prettier 
VS Code에서 F1 -> format입력 -> Enter
.prettierrc 설정파일을 생성하여 옵션 설정 가능

Prettier Option 페이지 참고
<https://prettier.io/docs/en/options.html>

에디터 설정에서 format on save를 체크하여 저장시마다 자동 정리 할 수있음

3장
=============

컴포넌트를 선언하는 방식은 1. 함수형 컴포넌트 2. 클래스형 컴포넌트 두 가지가 있음    
두 가지의 큰 차이는 클래스형 컴포넌트의 경우 state 기능 및 라이프 사이클 기능을 사용할 수 있다는 것과 임의 메서드를 정의할 수 있다는 것   
※ 리액트 공식 문서에서는 함수형 컴포넌트 + Hooks의 사용을 권장!

함수형 컴포넌트 
```JS
import React from 'react';

function App() {
 const name = '리액트';
 return <div className="react">{name}</div>
}

export default App;
```

클래스형 컴포넌트
```JS
import React, { Component } from 'react';

class App extends Component {
 render() {
  const name = '리액트';
  return <div className="react">{name}</div>
 }
}

export default App;
```
* 함수형 컴포넌트의 장점
  * 클래스형 컴포넌트보다 선언하기 편함   
  * 클래스형 컴포넌트보다 메모리 자원을 덜 사용   
  * 빌드 후 배포할 때 결과물의 파일 크기가 더 작음 (사실상 별차이는 없는 부분)   

* 함수형 컴포넌트의 단점
  * state와 라이프사이클 API의 사용이 불가능하지만 Hooks 기능 도입으로 해결


* 클래스형 컴포넌트

클래스형 컴포넌트에서는 render함수가 꼭 있어야하고 그 안에 보여 주어야할 JSX를 return 해야함


[노트]

화살표 함수 

```js
function BlackDog() {
  this.name = '흰둥이';
  return {
    name: '검둥이',
    bark: function() {
     console.log(this.name + ':멍멍!'); //자신이 종속된 객체를 this로 가리켜 검둥이가 됨
    }
  }
}

const blackDog = new BlackDog();
blackDog.bark(); // 검둥이: 멍멍!
```

```js
function WhitekDog() {
  this.name = '흰둥이';
  return {
    name: '검둥이',
    bark: () => {
     console.log(this.name + ':멍멍!'); //자신이 종속된 인스턴스를 가리켜 흰둥이가 됨
    }
  }
}


const whiteDog = new WhiteDog();
whiteDog.bark(); // 흰둥이: 멍멍!
```

화살표 함수는 값을 연산하여 바로 반환해야 할 때 사용하면 가독성이 높아짐
따로 {}를 열어주지 않으면 연산한 값을 그대로 반환한다는 의미

```js
function twice(value) {
  return value * 2;
}

const triple = (value) => value *3
```

props
-------------

properties를 줄인 표현으로 컴포넌트 속성을 설정할 때 사용하는 요소   
해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 값을 설정함 

MyComponent.js
```js
const MyComponent = props => {
  return <div>My name is {props.name}.</div>
};
```

App.js (현재 부모 컴포넌트 되겠음)
```js
const App = () => {
  return <MyComponent name="Namy" />;
}
```
   
   
* defaultProps
props 값을 따로 지정하지 않았을 때 보여 줄 기본값

MyComponent.js
```js
const MyComponent = props => {
  return <div>My name is {props.name}.</div>
};

MyComponent.defaultProps = {
  name: 'default name'
};
```
   
   
* children
컴포넌트 태그 사이의 내용을 보여주는 props
   
App.js
```js
const App = () => {
  return <MyComponent>React</MyComponent>;
};
```

MyComponent.js
```js
const MyComponent = props => {
  return (
    <div>
      My name is {props.name}.
      children value is {props.children}. // <MyComponent>React</MyComponent> 안의 React 텍스트가 children이 됨
    </div>
  )
};
```
   
   
* 비구조화 할당 문법 (구조 분해 문법)   
props.name, props.children과 같이 중복되는 props.를 편하게 사용할 수 있어 더 짧은 코드로 사용 할 수 있음

MyComponent.js
```js
const MyComponent = props => {
  const { name, children } = props; //비구조화 할당 문법
  return (
    <div>
      My name is {name}. //props.을 제외하고 사용할 수 있음
      children value is {children}.
    </div>
  )
};
```

함수의 파라미터로 사용할 수 있으며   
함수의 파라미터가 객체라면 그 값을 바로 비구조화해서 사용할 수 있음

MyComponent.js
```js
const MyComponent = ({ name, children }) => {
  return (
    <div>
      My name is {name}. //props.을 제외하고 사용할 수 있음
      children value is {children}.
    </div>
  )
};
```
   
   
* propTypes를 통한 props 검증

추후 정리


state
-------------

컴포넌트 자체적으로 지닌 값으로 컴포넌트 내부에서 업데이트 할 수 있는 값

props는 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값
컴포넌트는 자신은 해당 props를 읽기 전용으로만 사용할 수 있음
props를 바꾸려면 부모 컴포넌트에서 바꾸어 주어야함 

리액트는 두 가지 종류의 state가 있음
클래스형 컴포넌트에는 state
함수형 컴포넌트에는 useState

Counter.js 생성

#### 클래스형 컴포넌트의 state

```JS
import React, { Component } from 'react';

class Counter extends Component {

  constructor(props) { //constructor: 컴포넌트의 생성자 메서드. super(props)를 반드시 호출
    super(props);

    //state의 초기 value 설정하기. 객체 형식이어야함 값이 여러개 있을 수 있음
    this.state = {
      number: 0,
      fixedNumber: 0
    };
  }

  render() {
    const { number, fixedNumber } = this.state; //state를 조회할 때는 this.state로 조회
    return (
      <div>
        <h1>{number}</h1>
        <h2>바뀌지 않는 값: { fixedNumber }</h2>
        <button
          // onClick를 통해 버튼이 클릭 되었을 때 호출할 함수를 지정함
          onClick={() => {
            //this.setState를 사용하여 state에 새로운 값을 넣을 수 있음
            this.setState({ number: number + 1 });
          }}
        >
        +1
        </button>
      </div>
    );
  }
}
export default Counter;
```

* 다른 방식으로 state 초깃값 지정하기 
state를 constructor에서 꺼내기


```JS
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    number: 0,
    fixedNumber: 0
  }
  
  render() {
    const { number } = this.state; //state를 조회할 때는 this.state로 조회
    return (
     ...
    );
  }
}
export default Counter;
```


* this.setState에 객체 대신 함수 인자 전달하기

onClick 내부에서 this.setState를 두 번 호출 하는 경우

```JS
onClick={() => {
  //this.setState를 사용하여 state에 새로운 값을 넣을 수 있음
  this.setState({ number: number + 1 });
  this.setState({ number: this.state.number +1 });
  //두 번 사용하는 것임에도 버튼을 클릭할 때 1씩 더해짐
}}
```


위의 경우 해결책은 this.setState를 사용할 때 객체 대신 함수를 인자로 넣어 주는 것

```JS
this.setState((prevState, props) => {
  return {
   // 업데이트하고 싶은 내용
  }
})
```

prevState는 기존 상태
props는 현재 지니고 있는 props를 가리킴
props가 필요하지 않다면 생략 가능 

```JS
<button
  // onClick를 통해 버튼이 클릭 되었을 때 호출할 함수를 지정함
  onClick={() => {

    this.setState(prevState => {
      return {
        number: prevState.number + 1
      };
    });

    // 위 코드와 아래코드는 완전히 동일한 기능을 함
    // 아래코드는 함수에서 바로 객체를 반환 한다는 의미 {}를 생략함

    this.setState(prevState => ({
      number: prevState.number + 1
    }));

   }}
>
+1
</button>
```
 
화살표 함수에서 값을 반환하고 싶다면 코드 블록 { } 생략 가능

```JS
const sum = (a, b) => a + b;
```


* this.setState가 끝난 후 특정 작업 실행하기

setState의 두번째 파라미터로 콜백(callback)함수를 등록하여 작업을 처리할 수 있음

```JS
<button
  // onClick를 통해 버튼이 클릭 되었을 때 호출할 함수를 지정함
  onClick={() => {
    this.setState(
    {
      number: number + 1
    },
    () => {
      console.log('방금 setState가 호출되었습니다.');
      console.log(this.state);
     }
    );
  }}
>
  +1
</button>
```

#### 함수형 컴포넌트에서 useState 사용하기


* 배열 비구조화 할당

배열 비구조화 할당 문법을 알면 useState 사용 방법을 이해할 수 있음

```JS
const array = [1, 2];
const one = array[0];
const two = array[1];

// 위 코드를 비구조화 할당 
const array = [1, 2];
const [one, two] = array;
```

* useState 사용하기   
한 컴포넌트에서 useState 여러 번 사용할 수 있음 

Say.js 생성

```JS
import React, {useState} from 'react';

const Say = () => {
  // useState 함수 인자에는 상태의 초기 value
  // 함수를 호출하면 배열이 반환됨
  // 첫번째(message)는 현재 상태 두번째(setMessage)는 상태를 바꾸어 주는 함수. 세터(Setter)
  const [message, setMessage] = useState('');
  const onClickEnter = () => setMessage('안녕하세요');
  const onClickLeave = () => setMessage('안녕히 가세요!');
  
  const [color, setColor] = useState('black');

  return (
    <div>
      <button onClick={onClickEnter}>입장</button>
      <button onClick={onClickLeave}>퇴장</button>
      
      <h1 style={{ color }}>{message}</h1>

      <button style={{ color: 'red' }} onClick={() => setColor('red')}> 
       RED
      </button>
      <button style={{ color: 'green' }} onClick={() => setColor('green')}>
       Green
      </button>
      <button style={{ color: 'blue' }} onClick={() => setColor('blue')}>
       Blue
      </button>
    </div>
  );
};

export default Say;
```


state를 사용할 때 주의 사항
-------------
state값을 바꾸어야 할 때는 setState 혹은 useState를 통해 전달받은 세터 함수를 사용해야함

잘못된 코드 예 

```JS
// 클래스형 컴포넌트
this.state.number = this.state.number + 1;
this.state.array = this.array.push(2);
this.state.object.value = 5;

// 함수형 컴포넌트
const [object, setObject] = useState({ a: 1, b: 1 });
object.b = 2;
```

배열이나 객체를 업데이트해야 할 때는 배열이나 객체 사본을 만들고 그 사본의 값을 업데이트 한 후 사본의 상태를 setState 혹은 세터 함수를 통해 업데이트함

예시

```JS
// 객체 다루기 
const object = { a: 1, b: 2, c: 3 };
const nextObject = { ...object, b: 2 }; // 사본을 만들어서 b 값만 덮어 쓰기

// 배열 다루기
const array = [
 { id: 1, value: true },
 { id: 2, value: true },
 { id: 3, value: false }
];

let nextArray = array.concat({ id: 4 }); //새 항목 추가
nextArray.filter(item => item.id !==2); //id 2인 항목 제거
nextArray.map(item => (item.id === 1 ? { ...item, value: false } : item)); //id가 1인 항목의 value를 false로 설정
```
객체의 사본을 만들때는 spread 연산자 ...을 사용하고 배열에 대한 사본은 배열의 내장 함수들을 활용

정리
-------------
props는 부모 컴포넌트가 설정
state는 컴포넌트 자체적으로 지닌 값으로 컴포넌트 내부에서 값을 업데이트 할 수 있음

props는 무조건 고정적이 아니고 
부모 컴포넌트의 state를 자식 컴포넌트의 props로 전달하고 
자식 컴포넌트에서 특정 이벤트가 발생할 때 부모 컴포넌트의 메서드를 호출하면 props도 유동적으로 사용 가능





4장 
=============

사용자가 웹 브라우저에서 DOM요소들과 상호 작용하는 것을 이벤트라고 함

리액트의 이벤트 시스템 
-------------

이벤트 사용시 주의 사항

* 이벤트 이름은 카멜표기법으로 작성한다   
onClick, onKeyUp

* 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아닌 함수 형태의 값을 전달   
화살표 함수 문법으로 함수를 만들어 전달하거나 렌더링 부분 외부에 미리 만들어서 전달해도 됨 

* DOM 요소에만 이벤트를 설정할 수 있음   
div, button, input, span 등 DOM요소에 이벤트 설정   
직접 만든 컴포넌트에는 이벤트를 자체적으로 설정할 수 없음    

리액트에서 지원하는 이벤트 종류   
<https://ko.reactjs.org/docs/events.html>


예제로 이벤트 핸들링 익히기
-------------

* 컴포넌트 생성 및 불러오기

EventPractive.js 파일 생성

```JS
import React, { Component } from 'react';

class EventPractice extends Component {
  render() {
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input 
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          onChange={
            (e) => {
              console.log(e);
              console.log(e.target.value);
            }
          }
        />

      </div>
    );
  }
}

export default EventPractice;
```
   
* onChange 이벤트 핸들링하기   
   
e 객체는 SyntheticEvent로 웹 브라우저의 네이티브 이벤트를 감싸는 객체
네이티브 이벤트와 인터페이스가 같음 
SyntheticEvent는 네이티브 이벤트와 달리 이벤트가 끝나고 나면 이벤트가 초기화 되어 정보를 참조 할 수 없음
   
state에 input 값 담기

```JS
import React, { Component } from 'react';

class EventPractice extends Component {

  state = {
    message: ""
  }

  render() {
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input 
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          value={this.state.message}
          onChange={
            (e) => {
              this.setState({
                message: e.target.value
              })
            }
          }
        />

      </div>
    );
  }
}

export default EventPractice;
```
   
버튼을 누를 때 comment 값을 공백으로 설정   
   
```JS
import React, { Component } from 'react';

class EventPractice extends Component {
  
  state = {
    message: ""
  }

  render() {
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input 
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          value={this.state.message}
          onChange={
            (e) => {
              this.setState({
                message: e.target.value
              })
            }
          }
        />
        <button onClick={
          () => {
            alert(this.state.message);
            this.setState({
              message: ''
            });
          }
        }>확인</button>
      </div>
    );
  }
}

export default EventPractice;
```
   
* 임의 메서드 만들기   
   
이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라 함수 형태의 값을 전달해야함

위에서 이벤트를 처리할 때 렌더링을 하는 동시에 함수를 만들어서 전달해 주었고   
함수를 미리 준비하여 전달하는 방법도 있음   
성능상의 차이는 없지만 가독성은 훨씬 높다

위에서 onChange와 onClick에 전달한 함수를 따로 빼내 컴포넌트 임의 메서드를 만들어 보자

함수가 호출될 때 this는 호출부에 따라 결정되므로 클래스의 임의 메서드가 특정 HTML요소의 이벤트로 등록되는 과정에서   
메서드와 this의 관계가 끊어져 버림   
이 때문에 임의 메서드가 이벤트로 등록되어도 this를 컴포넌트 자신으로 제대로 가리키기 위해서는   
메서드를 this와 바인딩하는 작업이 필요하다   


기본방식

```JS
import React, { Component } from 'react';

class EventPractice extends Component {
  
  state = {
    message: ""
  }

  constructor(props) {
    super(props);
    // this가 컴포넌트 자신으로 제대로 가르키기 위해서 메서드를 this와 바인딩해야함
    this.handleChange = this.handleChange.bind(this);
    this.handleClick = this.handleClick.bind(this);
  };
  
  // 임의 메서드
  handleChange(e) {
    this.setState({
      message: e.target.value
    });
  }

  handleClick() {
    alert(this.state.message);
    this.setState({
      message: ''
    });
  }

  render() {
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input 
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          value={this.state.message}
          onChange={this.handleChange} // 임의 메서드 등록
        />
        <button onClick={this.handleClick}>확인</button>
      </div>
    );
  }
}

export default EventPractice;
```

Property Initializer Syntax를 사용한 메서드 작성   

메서드 바인딩은 생성자 메서드에서 하는 것이 정석이지만 불편할 수도 있음   
새 메서드를 만들 때마다 constructor도 수정해야하기 때문
바벨의 transform-class-properties 문법을 사용하면 화살표 함수 형태로 메서드를 정의 할 수 있음 

```JS
import React, { Component } from 'react';

class EventPractice extends Component {
  
  state = {
    message: ""
  }
  
  //constructor 삭제
  
  
  handleChange = (e) => { // 화살표 함수 형식으로 간단하게 변경
    this.setState({
      message: e.target.value
    });
  }

  handleClick = () => { // 화살표 함수 형식으로 간단하게 변경
    alert(this.state.message);
    this.setState({
      message: ''
    });
  }

  render() {
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input 
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          value={this.state.message}
          onChange={this.handleChange}
        />
        <button onClick={this.handleClick}>확인</button>
      </div>
    );
  }
}

export default EventPractice;
```

* input 여러 개 다루기 & onKeyPress 이벤트 핸들링하기

event 객체를 활용   
e.target.name은 해당 인풋의 name을 가리킴 이 값을 사용하여 state를 설정

```JS
import React, { Component } from 'react';

class EventPractice extends Component {
  
  state = {
    username: '', // 2. state 에 username 값 추가
    message: ''
  }

  handleChange = (e) => { // 3. handleChange 변경
    this.setState({
      [e.target.name]: e.target.value
      /*
      4. 객체 안에서 []로 감싸면 그 안에 넣은 레퍼런스가 가리키는 실제 값이 key 값으로 사용됨
      각 input 태그에 설정된 name="username", name="message"의 username, message가 키 값이 되어
      아래와 같은 형태로 되는 것임 
      {
       'username': e.target.value
      }
      */
    });
  }

  handleClick = () => {
    alert(this.state.username + ': ' + this.state.message);
    this.setState({
      username: '',
      message: ''
    });
  }
  
  handleKeyPress = (e) => {
    if(e.key === 'Enter') {
      this.handleClick();
    }
  }

  render() { // 1. name 값이 username인 input을 렌더링
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input 
          type="text"
          name="username"
          placeholder="사용자명"
          value={this.state.username}
          onChange={this.handleChange}
        />
        <input 
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          value={this.state.message}
          onChange={this.handleChange}
          onKeyPress={this.handleKeyPress}
        />
        <button onClick={this.handleClick}>확인</button>
      </div>
    );
  }
}

export default EventPractice;
```

4. 추가 설명 


```JS
const name = 'variantKey';
const object = {
 [name]: 'value'
};
```
위 코드의 결과는 다음과 같다   
```JS
{
 'variantKey': 'value'
}
```



함수형 컴포넌트로 구현해 보기 
-------------

위의 작업을 함수형 컴포넌트로 구현할 수 있음

```JS
import React, { useState } from 'react';

const EventPracticeComponent = () => {
  const [username, setUsername] =  useState('');
  const [message, setMessage] = useState('');
  const onchangeUserName = e => setUsername(e.target.value);
  const onChangeMessage = e => setMessage(e.target.value);
  const onClick = () => {
    alert(username + ': ' + message);
    setUsername('');
    setMessage('');
  };

  const onKeyPress = e => {
    if(e.key === 'Enter') {
      onClick();
    }
  };

  return (
    <div>
      <h1>이벤트 연습</h1>
      <input 
          type="text"
          name="username"
          placeholder="사용자명"
          value={username}
          onChange={onchangeUserName}
      />
      <input 
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          value={message}
          onChange={onChangeMessage}
          onKeyPress={onKeyPress}
      />
      <button onClick={onClick}>확인</button>
    </div>
    );
};

export default EventPracticeComponent;
```


useState를 통해 사용하는 상태에 문자열이 아닌 객체를 넣어 보자
인풋 개수가 많아지면 e.target.name을 활용하는 것이 더 좋을 수 있음

```JS
import React, { useState } from 'react';

const EventPractice = () => {
  const [form, setForm] = useState({
    username: '',
    message: ''
  });
  
  // e.target.name 값을 활용하려면 인풋값이 들어 있는 form 객체를 사용
  const { username, message } = form; 
  const onChange = e => {
    const nextForm = {
      ...form, // 기존의 form 내용을 이 자리에 복사한 뒤
      [e.target.name]: e.target.value // 원하는 값을 덮어 씌우기
    };
    setForm(nextForm);
  };

  const onClick = () => {
    alert(username + ': ' + message);
    setForm({
      username: '',
      message: ''
    });
  };

  const onKeyPress = e => {
    if(e.key === 'Enter') {
      onClick();
    }
  };

  return (
    <div>
      <h1>이벤트 연습</h1>
      <input 
          type="text"
          name="username"
          placeholder="사용자명"
          value={username}
          onChange={onChange}
      />
      <input 
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          value={message}
          onChange={onChange}
          onKeyPress={onKeyPress}
      />
      <button onClick={onClick}>확인</button>
    </div>
    );
};

export default EventPractice;
```


5장 
=============




6장 
=============
