# 리액트를 다루는 기술

## 2장 JSX

리액트는 뷰만 신경쓰는 라이브러리라고 할 있음    
프레임 워크는 Ajax, 데이터 모델링, 라우팅 등의 기능을 내장하고 있음   

yarn은 npm을 대체 할 수 있는 도구로 npm보다 빠르며 효율적인 캐시 시스템과 기타 부가기능을 제공 하고 있음   

#### 2.4.3 If 문 대신 조건부 연산자   
JSX 내부의 자바스크립트 표현식에서 if문을 사용할 수 없지만 {} 안에 조건부 연산자, 즉 삼항 연산자를 사용할 수 있음

#### 2.4.4 AND 연산자(&&)를 사용한 조건부 렌더링  
- 특정 조건을 만족할 때 내용을 보여주고 아닐 때 아예 아무것도 렌더링 하지 않아야 할 경우
```js
{name === 'react' && <h1>react!</h1> : null}
```
- 위의 경우를 &&(AND)를 사용하여 더 짧게 표현 
```js
{name === 'react' && <h1>react</h1>
```
falsy한 값인 0은 예외적으로 화면에 나타남

#### 2.4.5 undefined를 렌더링하지 않기   
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
### 2.5 ESLint와 Prettier 적용하기    


#### 2.5.2 Prettier    
VS Code에서 F1 -> format입력 -> Enter   
.prettierrc 설정파일을 생성하여 옵션 설정 가능   

Prettier Option 페이지 참고   
<https://prettier.io/docs/en/options.html>

에디터 설정에서 format on save를 체크하여 저장시마다 자동 정리 할 수있음

## 3장 컴포넌트

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

### 3.3 props

properties를 줄인 표현으로 컴포넌트 속성을 설정할 때 사용하는 요소   
해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 값을 설정함   
props 이름만 넣어주면 propsName={true} 와 동일한 의미   

#### 3.3.1 JSX 내부에서 props 렌더링

MyComponent.js
```js
const MyComponent = props => {
  return <div>My name is {props.name}.</div>
};
```
#### 3.3.2 컴포넌트를 사용할 때 props 값 지정하기   

App.js (현재 부모 컴포넌트 되겠음)
```js
const App = () => {
  return <MyComponent name="Namy" />;
}
```
#### 3.3.3 props 기본값 설정: defaultProps   
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
   
#### 3.3.4 태그 사이의 내용을 보여주는 children
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
   
#### 3.3.5 비구조화 할당 문법을 통해 props 내부 값 추출하기   
비구조화 할당 문법 (구조 분해 문법)     
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
   
   
#### 3.3.6 propTypes를 통한 props 검증   

##### 3.3.6.1 isRequired를 사용하여 필수 propTypes 설정   

##### 3.3.6.2 더 많은 propTypes 종류   


추후 정리


### 3.4 state

컴포넌트 자체적으로 지닌 값으로 컴포넌트 내부에서 업데이트 할 수 있는 값

props는 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값
컴포넌트는 자신은 해당 props를 읽기 전용으로만 사용할 수 있음
props를 바꾸려면 부모 컴포넌트에서 바꾸어 주어야함 

리액트는 두 가지 종류의 state가 있음
클래스형 컴포넌트에는 state
함수형 컴포넌트에는 useState

Counter.js 생성

#### 3.4.1 클래스형 컴포넌트의 state, 3.4.1.1 state 객체 안에 여러 값이 있을 때

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

##### 3.4.1.2 state를 constructor에서 꺼내기   

다른 방식으로 state 초깃값 지정하기 

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

##### 3.4.1.3 this.setState에 객체 대신 함수 인자 전달하기   
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


##### 3.4.1.4 this.setState가 끝난 후 특정 작업 실행하기

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

#### 3.4.2 함수형 컴포넌트에서 useState 사용하기


##### 3.4.2.1 배열 비구조화 할당

배열 비구조화 할당 문법을 알면 useState 사용 방법을 이해할 수 있음

```JS
const array = [1, 2];
const one = array[0];
const two = array[1];

// 위 코드를 비구조화 할당 
const array = [1, 2];
const [one, two] = array;
```

##### 3.4.2.2 useState 사용하기, 3.4.2.3 
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


### 3.5 state를 사용할 때 주의 사항
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

### 3.6 정리   
props는 부모 컴포넌트가 설정
state는 컴포넌트 자체적으로 지닌 값으로 컴포넌트 내부에서 값을 업데이트 할 수 있음

props는 무조건 고정적이 아니고 
부모 컴포넌트의 state를 자식 컴포넌트의 props로 전달하고 
자식 컴포넌트에서 특정 이벤트가 발생할 때 부모 컴포넌트의 메서드를 호출하면 props도 유동적으로 사용 가능


## 4장 이벤트 핸들링

사용자가 웹 브라우저에서 DOM요소들과 상호 작용하는 것을 이벤트라고 함

### 4.1 리액트의 이벤트 시스템 

#### 4.1.1 이벤트 사용시 주의 사항

* 이벤트 이름은 카멜표기법으로 작성한다   
onClick, onKeyUp

* 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아닌 함수 형태의 값을 전달   
화살표 함수 문법으로 함수를 만들어 전달하거나 렌더링 부분 외부에 미리 만들어서 전달해도 됨 

* DOM 요소에만 이벤트를 설정할 수 있음   
div, button, input, span 등 DOM요소에 이벤트 설정   
직접 만든 컴포넌트에는 이벤트를 자체적으로 설정할 수 없음    

#### 4.1.2 리액트에서 지원하는 이벤트 종류   
<https://ko.reactjs.org/docs/events.html>


### 4.2 예제로 이벤트 핸들링 익히기

#### 4.2.1 컴포넌트 생성 및 불러오기

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
   
#### 4.2.2 onChange 이벤트 핸들링하기   
   
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
   
#### 4.2.3 임의 메서드 만들기   
   
이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라 함수 형태의 값을 전달해야함

위에서 이벤트를 처리할 때 렌더링을 하는 동시에 함수를 만들어서 전달해 주었고   
함수를 미리 준비하여 전달하는 방법도 있음   
성능상의 차이는 없지만 가독성은 훨씬 높다

위에서 onChange와 onClick에 전달한 함수를 따로 빼내 컴포넌트 임의 메서드를 만들어 보자

함수가 호출될 때 this는 호출부에 따라 결정되므로 클래스의 임의 메서드가 특정 HTML요소의 이벤트로 등록되는 과정에서   
메서드와 this의 관계가 끊어져 버림   
이 때문에 임의 메서드가 이벤트로 등록되어도 this를 컴포넌트 자신으로 제대로 가리키기 위해서는   
메서드를 this와 바인딩하는 작업이 필요하다   


##### 4.2.3.1 기본방식

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

##### 4.2.3.2 Property Initializer Syntax를 사용한 메서드 작성   

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

#### 4.2.4 input 여러 개 다루기 & 4.2.5 onKeyPress 이벤트 핸들링하기

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



### 4.3 함수형 컴포넌트로 구현해 보기 

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

리액트 상태에서 객체를 수정해야 할 때에는,   
새로운 객체를 만들어서 새로운 객체에 변화를 주고, 이를 상태로 사용해주어야 함   

```JS
const nextForm = {
  ...form, // 기존의 form 내용을 이 자리에 복사한 뒤
  [e.target.name]: e.target.value // 원하는 값을 덮어 씌우기
};
```

... 는 spread 문법   
객체의 내용을 모두 "펼쳐서" 기존 객체를 복사   
이러한 작업을, "불변성을 지킨다" 라고 부름.    
불변성을 지켜주어야만 리액트 컴포넌트에서 상태가 업데이트가 됐음을 감지 할 수 있고 이에 따라 필요한 리렌더링이 진행됨   
추가적으로, 리액트에서는 불변성을 지켜주어야만 컴포넌트 업데이트 성능 최적화를 제대로 할 수 있음

## 5장 ref: DOM에 이름 달기

### 5.1 ref는 어떤 상황에서 사용해야 할까?

일반 HTML에서 DOM요소에 이름을 달 때 id를 사용하는 것처럼 리액트 내부에서 DOM에 이름을 다는 것   
reference의 줄임말. DOM을 직접적으로 건드려야 할 때 사용   
   
   
ValidationSample.js 생성 (
```JS
import React, { Component } from "react";
import './ValidationSample.css'

class ValidationSample extends Component {
  state = {
    password: '',
    clicked: false,
    validated: false
  }

  handleChange = (e) => {
    this.setState({
      password: e.target.value
    });
  }

  handleButtonClick = () => {
    this.setState({
      clicked: true,
      validated: this.state.password === '000'
    });
  }

  render() {
    return (
      <div>
        <input
          type="password"
          value={this.state.password}
          onChange={this.handleChange}
          className={this.state.clicked ? (this.state.validated ? 'success' : 'failure') : ''} 
        />
        <button onClick={this.handleButtonClick}>검증하기</button>
      </div>
    );
  }
}

export default ValidationSample;
```
   
App.js 는 클래스형 컴포넌트로 전환
함수형 컴포넌트에서 ref를 사용하려면 Hooks를 사용해야 하기 때문에 

```JS
import React, { Component } from "react";
import ValidationSample from './ValidationSample';

class App extends Component {
  render() {
    return (
      <ValidationSample />
    );
  }
}

export default App;
```
   
#### 5.1.3 DOM을 꼭 사용해야하는 상황 (state만으로 해결할 수 없는 기능이 있음)
아래외 같은 상황은 ref를 사용 
   
* 특정 input에 포커스 추가
* 스크롤 박스 조작하기
* Canvas 요소에 그림 그리기 등 
   
   
### 5.2 ref 사용

* 콜백 함수를 통한 ref 설정
ref를 달고자 하는 요소에 ref라는 콜백 함수를 props로 전달해줌   
콜백 함수는 ref 값을 파라미터로 전달받고 함수 내부에서 파라미터로 받은 ref를 컴포넌트의 멤버 변수로 설정    

예시
```JS
<input ref={(ref) => {this.input}} />
```
   
   
#### 5.2.2 createRef를 통한 ref 설정
리액트에 내장되어 있는 createRef라는 함수를 사용하는 것 
이 함수를 사용하면 더 적은 코드로 쉽게 사용할 수 있음 

createRef 사용 예시
```JS
import React, { Component } from "react";

class RefSample extends Component {
 input = React.createRef(); // 1. 컴포넌트 내부에서 변수로 createRef를 담아주어야함 
 
 handleFocus = () => {
  this.input.current.focus(); // 3. ref를 설정해 준 DOM에 접근하려면 this.input.current를 조회함
 }
 
 render() {
  return (
   <div>
    <input ref={this.input} /> // 2. ref를 달고자 하는 요소에 ref props로 넣어주면 설정 완료
   </div>
  );
 }
}

export default RefSample;
```
   
ValidationSample.js 에 ref 적용하기
```JS
class ValidationSample extends Component {
  state = {
    password: '',
    clicked: false,
    validated: false
  }

  handleChange = (e) => {
    this.setState({
      password: e.target.value
    });
  }

  handleButtonClick = () => {
    this.setState({
      clicked: true,
      validated: this.state.password === '000'
    });
    this.input.focus(); // 추가된 코드
  }

  render() {
    return (
      <div>
        <input
          type="password"
          value={this.state.password}
          onChange={this.handleChange}
          className={this.state.clicked ? (this.state.validated ? 'success' : 'failure') : ''} 
          ref={(ref) => this.input=ref} // 추가된 코드
        />
        <button onClick={this.handleButtonClick}>검증하기</button>
      </div>
    );
  }
}
```
   
### 5.3 컴포넌트에 ref달기
   
주로 컴포넌트 내부에 있는 DOM을 컴포넌트 외부에서 사용할 때 씀

#### 5.3.1 사용법 

```JS
<MyComponent
 ref={(ref) => {this.myComponent=ref}}
 /*
 컴포넌트의 내부 메서드 및 멤버 변수에도 접근할 수 있음
 즉, 내부의 ref에도 접근 할 수 있다 (예: myComponent.handleClick, myComponent.input 등)
 */
/>
```
   
ScrollBox.js 생성
```JS
import React, { Component } from "react";

class ScrollBox extends Component {

  scrollToBottom = () => {
    const { scrollHeight, clientHeight } = this.box;
    /*
    비구조화 할당 문법 사용했고 아래와 같은 의미
    const scrollHeight = this.box.scrollHeight;
    const clientHeight = this.box.clientHeight; 
    */
   this.box.scrollTop = scrollHeight - clientHeight;
  }
  // scrollToBottom 메서드는 부모 컴포넌트인 APP 컴포넌트에서 ScrollBox에 ref를 달면 사용할 수 있음
  
  render() {
    const style = {
      border: '1px solid black',
      height: '300px',
      width: '300px',
      overflow: 'auto',
      position: 'relative'
    };

    const innnerStyle = {
      width: '100%',
      height: '650px',
      background: 'linear-gradient(white, black)'
    }

    return (
      <div
        style={style}
        ref={(ref) => {this.box=ref}}>
        <div style={innnerStyle} />
      </div>
    );
  }
}

export default ScrollBox;
```
   
App.js
```JS
class App extends Component {
  render() {
    return (
      <div>
        <ScrollBox ref={(ref) => this.scrollBox=ref}/>
        <button onClick={() => this.scrollBox.scrollToBottom()}> 
	/*
        onClick = {this.scrollBox.scrollBottom}으로 작성해도 틀린 것은 아니나
        컴포넌트가 처음 렌더링 될 때 this.scrollBox 값이 undefined이므로 
        this.scrollBox.scrollToBottom 값을 읽어 오는 과정에서 오류가 발생함
        화살표 함수 문법을 사용하여 아예 새로운 함수를 만들고 내부에서 this.scrollBox.scrollToBottom 메서드를 실행하면 
        버튼을 누를 때 (이미 한 번 렌더링을 해서 this.scrollBox를 설정한 시점)
        this.scrollBox.scrollToBottom 값을 읽어 와서 실행하므로 오류가 발생하지 않음 
        */
          맨 밑으로
        </button>
      </div>
    );
  }
}
```
   
### 5.4 정리

컴포넌트 내부에서 DOM에 직접 접근해야 할 때는 ref를 사용함   
다른 컴포넌트끼리 데이터를 교류할 때 사용하는 것은 잘못됨
   
   
   
## 6장 컴포넌트의 반복

```HTML
<ul>
  <li>...</li>
  <li>...</li>
  <li>...</li>
</ul>
```
위와 같이 반복되는 내용을 효율적으로 보여 주고 관리하는 방법

### 6.1 자바스크립트 배열의 map()함수   

자바스크립트 배열 객체의 내장 함수 map()을 사용하여 반복되는 컴포넌트를 렌더링 할 수 있다   
map 함수에 파라미터로 전달된 함수를 사용해서      
배열 내 각 요소를 원하는 규칙(callback에 정의한)에 따라 변환한 결과로 새로운 배열을 생성함   
배열의 각 요소에 대해 실행한 callback의 결과를 모은 새로운 배열   
즉, 기존 배열을 새로운 배열로 만든다   

#### 6.1.1 문법
```JS
arr.map(callback, [thisArg])
arr.map(callback(currentValue[, index[, array]])[, thisArg]) //MDN
```
   
함수의 파라미터
* callback: 새로운 배열의 요소를 생성하는 함수로 파라미터는 다음 세가지   
  * currentValue: 현재 처리하고 있는 요소   
  * index: 현재 처리하고 있는 요소의 index 값   
  * array: 현재 처리하고 있는 원본 배열, map()을 호출한 배열   

* thisArg(선택 항목): callback 함수 내부에서 사용할 this 레퍼런스, callback을 실행할 때 this로 사용되는 값   

   
### 6.2 데이터 배열을 컴포넌트 배열로 변환하기   

IterationSample.js 생성

```JS
import React from "react";

const IterationSample = () => {
  const names = ['눈사람', '얼음', '눈', '바람'];
  const nameList = names.map(name => <li>{name}</li>); // currentValue는 name. 새로 생성된 배열을 nameList에 담는다
  return <ul>{nameList}</ul>;
}

export default IterationSample;
```
위 코드를 실행하면 Key props이 없다는 경고가 나옴

### 6.3 key

리액트에서 key는 컴포넌트 배열을 렌더링했을 때 어떤 원소에 변동이 있었는지 알아내려고 사용   
key가 없을 때는 가상돔을 비교하는 과정에서 리스트를 순차적으로 비교하면서 변화를 감지하지만   
key가 있다면 이 값을 사용하여 어떤 변화가 일어났는지 더욱 빠르게 알아낼 수 있음

#### 6.3.1 key 설정

key 값을 설정할 때는 map 함수의 인자로 전달되는 함수 내부에서 컴포넌트 props를 설정하듯이 설정하고   
key 값은 언제나 유일해야하므로 데이터가 가진 고유값을 key값으로 설정해야함  

바로 위 예제를 다음과 같이 수정 

IterationSample.js
```JS
import React from "react";

const IterationSample = () => {
  const names = ['눈사람', '얼음', '눈', '바람'];
  const namesList = names.map((name, index) => <li key={index}>{name}</li>); //currentValue: name, index: index
  // index를 key로 사용하면 배열이 변경될 때 효율적으로 렌더링 하지 못하기 때문에 고유한 값이 없을 때만 index 값을 key로 사용한다
 
  return <ul>{namesList}</ul>;
}

export default IterationSample;
```
   

### 6.4 응용 

#### 6.4.1 초기 상태 설정하기
useState를 사용하여 초기상태 설정 
   
세 가지 상태를 사용함 (1. 데이터 배열, 2. input 상태, 3. 데이터 배열에서 새로운 항목을 추가할 때 사용할 고유 id)   

IterationSample.js
```JS
import React, { useState } from "react";

const IterationSample = () => {
  const [names, setNames] = useState([
    {id: 1, text: '눈사람'}, // 객체 형태의 배열
    {id: 2, text: '얼음'},
    {id: 3, text: '눈'},
    {id: 4, text: '바람'}
  ]);
  
  const [inputText, setInputText] = useState('');
  const [nextId, setNextId] = useState(5); // 새로운 항목을 추가할 때 사용할 id

  const namesList = names.map(name => <li key={name.id}>{name.text}</li>);
  return <ul>{namesList}</ul>;
}

export default IterationSample;
```
    
#### 6.4.2 데이터 추가 기능 구현하기    
```JS
import React, { useState } from "react";

const IterationSample = () => {
  // useState에서 지정한 값은 [1, 2] 1에 들어감
  const [names, setNames] = useState([
    {id: 1, text: '눈사람'}, // 객체 형태의 배열 useState의 names가 됨
    {id: 2, text: '얼음'},
    {id: 3, text: '눈'},
    {id: 4, text: '바람'}
  ]);

  const [inputText, setInputText] = useState('');
  const [nextId, setNextId] = useState(5); // 새로운 항목을 추가할 때 사용할 id

  const onChange = e => setInputText(e.target.value);
  const onClick = () => {
    const nextNames = names.concat({ // concat은 새로운 배열을 만들어줌. push는 기존 배열 자체를 변경함 (불변성 유지)
      id: nextId, // nextId 값을 id로 설정하고
      text: inputText
    });
    setNextId(nextId + 1); // nextId 값에 1을 더해 준다.
    setNames(nextNames); // names 값을 업데이트 한다.
    setInputText(''); // inputText를 비운다.
  }

  const namesList = names.map(name => <li key={name.id}>{name.text}</li>);
  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>추가</button>
      <ul>{namesList}</ul>
    </>
  ); 
};

export default IterationSample;
```
불변성 유지   
리액트에서 상태를 업데이트할 때는 기존 상태를 그대로 두면서 새로운 값을 상태로 설정해야함    
불변성 유지를 해 주어야 컴포넌트의 성능을 최적화 할 수 있음 


#### 6.4.3 데이터 제거 기능 구현하기      
불변성을 유지하면서 배열의 특정 항목을 지울 때는 배열 내장 함수 filter를 사용함

예시)
```JS
const numbers = [1, 2, 3, 4, 5, 6];
const withoutThree = numbers.filter(number => number !==3);
// 결과: [1, 2, 4, 5, 6]
```

```JS
const IterationSample = () => {
  // useState에서 지정한 값은 [1, 2] 1에 들어감
  const [names, setNames] = useState([
    {id: 1, text: '눈사람'}, // 객체 형태의 배열 useState의 names가 됨
    {id: 2, text: '얼음'},
    {id: 3, text: '눈'},
    {id: 4, text: '바람'}
  ]);

  const [inputText, setInputText] = useState('');
  const [nextId, setNextId] = useState(5); // 새로운 항목을 추가할 때 사용할 id

  const onChange = e => setInputText(e.target.value);
  const onClick = () => {
    const nextNames = names.concat({ // concat은 새로운 배열을 만들어줌. push는 기존 배열 자체를 변경함
      id: nextId, // nextId 값을 id로 설정하고
      text: inputText
    });
    setNextId(nextId + 1); // nextId 값에 1을 더해 준다.
    setNames(nextNames); // names 값을 업데이트 한다.
    setInputText(''); // inputText를 비운다.
  }
  const onRemove = id => {
    const nextNames = names.filter(name => name.id !== id);
    setNames(nextNames);
  }
  const namesList = names.map(name => ( // 추가 할 땐 없던 괄호가 생겼다.. 단순 코드 구분 때문인가.. 괄호가 없어도 실행은 된다
    <li key={name.id} 
    	onDoubleClick={() => onRemove(name.id)}
    >
      {name.text}
    </li>
  ));
  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>추가</button>
      <ul>{namesList}</ul>
    </>
  ); 
};
```


### 6.5 정리   

key값은 유일해야 한다. 중복되면 오류 발생   
상태 안에서 배열을 변형할 때는 배열에 직접 접근하여 수정하는 것이 아니라   
concat, filter 등의 배열 내장 함수를 사용하여 새로운 배열을 만든 후 새로운 상태로 설정해 주어야함   

## 7장 컴포넌트의 라이프사이클 메서드

모든 리액트 컴포넌트에는 라이프사이클(수명주기)가 존재   
컴포넌트의 수명은 페이지에 렌더링되기 전인 준비 과정에서 시작하여 페이지에서 사라질 때 끝남   
라이프사이클 메서드는 클래스형 컴포넌트에서만 사용할 수 있음   
함수형 컴포넌트에서는 Hooks 기능을 사용하여 비슷한 작업을 처리함   

### 7.1 라이프사이클 메서드의 이해

라이프사이클 메서드의 종류는 총 9가지이며 3 카테고리로 나눔  
Will 접두사가 붙은 메서드는 어떤 작업을 작동하기 전 실행   
Did 접두사가 붙은 메서드는 어떤 작업을 작동한 후에 실행   

#### 마운트 (mount)
DOM이 생성되고 웹 브라우저상에 나타나는 것

마운트할 때 호출하는 메서드   

* constructor   
컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자 메서드   

* getDerivedStateFromProps   
props에 있는 값을 state에 넣을 때 사용하는 메서드   

* render  
우리가 준비한 UI를 렌더링하는 메서드

* componentDidMount   
컴포넌트가 웹 브라우저상에 나타난 후 호출하는 메서드

####  업데이트 (update)
컴포넌트는 다음과 같은 총 네가지의 경우 업데이트함    
1. props가 바뀔 때
2. state가 바뀔 때
3. 부모 컴포넌트가 리렌더링될 때
4. this.forceUpdate로 강제로 렌더링을 트리거할 때

* 컴포넌트가 업데이트 되는 경우
  * 부모 컴포넌트에서 전달하는 props가 바뀔 때 렌더링
  * 컴포넌트 자신이 들고 있는 state가 setState를 통해 업데이트될 때
  * 부모 컴포넌트가 리렌더링 될 때: 자신에게 할당된 props가 바뀌지 않아도, 자신이 들고 있는 state가 바뀌지 않아도 부모 컴포넌트가 리렌더링되면 자식 컴포넌트 또한 리렌더링
   
업데이트할 때 호출하는 메서드

* getDerivedStateFromProps   
마운트 과정과 업데이트 시작 전에도 호출. props의 변화에 따라 state 값에도 변화를 주고 싶을 때 사용

* shouldComponentUpdate   
컴포넌트가 리렌더링을 해야 할지 말아야 할지 결정하는 메서드.    
이 메서드는 true/false 값을 반환해야 함   
true: 다음 라이프사이클 메서드 계속 실행   
false: 작업 중지. 컴포넌트가 리렌더링 되지 않음.    
특정 함수에서 this.forceUpdate()를 호출한다면 이 과정은 생략하고 render()호출   

* render
컴포넌트를 리렌더링함

* getSnapshotBeforeUpdate   
컴포넌트의 변화를 DOM에 반영하기 바로 직전에 호출하는 메서드

* componentDidUpdate   
컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드   
최초 렌더링에서는 호출되지 않음

#### 언마운트 (unmount)     
마운드의 반대 과정. 즉 컴포넌트를 DOM에서 제거하는 것  

언마운트할 때 호출하는 메서드      

* componentWillUnmount   
컴포넌트가 웹 브라우저상에서 사라지기 전에 호출하는 메서드


### 7.2 라이프사이클 메서드 살펴보기

<https://ko.reactjs.org/docs/react-component.html>

#### 7.2.1 render() 함수

```JS
render() {...}
```
클래스 컴포넌트에서 반드시 정의해아하는 유일한 메서드
컴포넌트 모양새를 정의함  
라이프사이클 메서드 중 유일한 필수 메서드
이 메서드 안에서 this.props와 this.state에 접근 할 수 있으며 리액트 요소를 반환
아무것도 보여 주고 싶지 않다면 null, false 값을 반환 

주의사항

render()안에서는 이벤드 설정이 아닌 곳에서 setState를 사용하면 안됨
브라우저 DOM에 접근도 안됨
DOM정보를 가져오거나 state에 변화를 줄 때는 componentDidMount에서 처리해야함 

#### 7.2.2 constructor 메서드   

```JS
constructor(props) {...}
```

컴포넌트 생성자 메서드로 컴포넌트를 만들 때 처음으로 실행    
초기 state를 정의할 수 있음   

생성자는 사용하는 두 가지 목적   

1. this.state에 객체를 할당하여 지역 state를 초기화
2. 인스턴스에 이벤트 처리 메서드를 바인딩

#### 7.2.3 getDerivedStateFromProps 메서드 (자주 사용하지 않음)   
props로 받아온 값을 state에 동기화시키는 용도로 사용   
컴포넌트가 최초 마운트될 때와 업데이트될 때 redder 호출 전에 호출     
state를 갱신하기 위한 객체를 반환하거나, null을 반환하여 아무 것도 갱신하지 않을 수 있습니다.

```JS
static getDerivedStateFromProps(nextProps, prevState) {
  // 여기서는 setState 를 하는 것이 아니라
  // 특정 props 가 바뀔 때 설정하고 설정하고 싶은 state 값을 리턴하는 형태로
  // 사용됩니다.
  /*
  if (nextProps.value !== prevState.value) { // 조건에 따라 특정 값 동기화 
    return { value: nextProps.value };
  }
  return null; // state를 변경할 필요가 없다면 null을 반환
  */
}
```

#### 7.2.4 componentDidMount 메서드

```JS
componentDidMount() {...}
```

컴포넌트를 만들고 첫 렌더링을 다 마친 후 실행   
DOM 노드가 있어야 하는 초기화 작업은 이 메서드에서 이루어지면 됨   
자바스크립트 라이브러리 또는 프레임워크의 함수를 호출하거나 이벤트 등록, setTimeOut, setInterval, 네트워크 요청 같은 비동기 작업을 처리함     
setState()를 호출하는 경우도 있음   
 
#### 7.2.5 shouldComponentUpdate 메서드 (자주 사용하지 않음)   

```JS
shouldComponentUpdate(nextProps, nextState) {...}
```
props나 state를 변경했을 때 리렌더링을 시작할지 여부를 지정하는 메서드
기본 동작은 매 state 변화마다 다시 렌더링을 수행
반드시 true, false값을 반환해야함   
이 메서드를 따로 생성하지 않으면 기본적으로 true 값을 반환   
false 값을 반환한다면 업데이트 과정은 여기서 중지됨   
현재 props는 this.props, state는 this.state로 접근   
새로 설정될 props 또는 state는 nextProps와 nextState로 접근 할 수 있음

성능 최적화만을 위한 메서드로 렌더링을 방지하는 목적으로 사용할 경우 버그로 이어짐 

#### 7.2.6 getSnapshotBeforeUpdate 메서드 (자주 사용하지 않음)    
render에서 만들어진 결과물이 브라우저에 실제로 반영되기 직전에 호출    
이 메서드에서 반환하는 값은 componentDidUpdate에서 세 번째 파라미터인 snapshot 값으로 전달 받을 수 있음   
주로 업데이트하기 직전의 값을 참고할 일이 있을 때 활용 

예시
```JS 
  getSnapshotBeforeUpdate(prevProps, prevState) {
    // DOM 업데이트가 일어나기 직전의 시점입니다.
    // 새 데이터가 상단에 추가되어도 스크롤바를 유지해보겠습니다.
    // scrollHeight 는 전 후를 비교해서 스크롤 위치를 설정하기 위함이고,
    // scrollTop 은, 이 기능이 크롬에 이미 구현이 되어있는데, 
    // 이미 구현이 되어있다면 처리하지 않도록 하기 위함입니다.
    if (prevState.array !== this.state.array) {
      const {
        scrollTop, scrollHeight
      } = this.list;

      // 여기서 반환 하는 값은 componentDidMount 에서 snapshot 값으로 받아올 수 있습니다.
      return {
        scrollTop, scrollHeight
      };
    }
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    if (snapshot) {
      const { scrollTop } = this.list;
      if (scrollTop !== snapshot.scrollTop) return; // 기능이 이미 구현되어있다면 처리하지 않습니다.
      const diff = this.list.scrollHeight - snapshot.scrollHeight;
      this.list.scrollTop += diff;
    }
  }
```

#### 7.2.7 componentDidUpdate 메서드   
```JS
componentDidUpdate(prevProps, prevState, snapshot) {...}
```
리렌더링 완료한 후 실행최초 렌더링에서는 호출되지 않음   
업데이트가 끝난 직후로 DOM 관련 처리를 해도 무방함    
컴포넌트가 갱신되었을 때 DOM을 조작하기 위하여 이 메서드를 활용함    
prevProps, prevState를 사용하여 컴포넌트가 이전에 가졌던 데이터에 접근 가능
이전과 현재의 props를 비교하여 네트워크 요청을 보내는 작업도 이 메서드에서 이루어지면 됨  
getSnapshotBeforeUpdate()에서 반환값이 있다면 이 메서드에서 세 번째 인자 snapshot로 값을 전달 받을 수 있음      
반환값이 없다면 해당 인자는 undefined   

#### 7.2.8 componentWillUnmount 메서드   
```JS
componentWillUnmount() {...}
```
컴포넌트가 DOM에서 제거되기 직전에 실행함
componentDidUpdate에서 등록한 이벤트, 타이머, 네트워크 요청 취소, 직접 생성한 DOM이 있다면 여기서 제거해야함

#### 7.2.9 componentDidCatch 메서드   
```JS
componentDidCatch(error, info) {
  this.setState({
    error: true
  });
}
```
컴포넌트 렌더링 도중에 에러가 발생했을 때 오류 UI를 보여 줄 수 있게 해줌   
자기 자신에게 발생하는 에러는 잡아낼 수 없고 자신의 this.props.children으로 전달되는 컴포넌트에서 발생하는 에러만 잡아낼 수 있다   
2개의 매개변수를 전달받음   

1. error - 발생한 오류   
2. info - 어떤 컴포넌트가 오류를 발생시켰는지에 대한 정보를 포함한 componentStack 키를 갖고 있는 객체   



### 7.3 라이프사이클 메서드 사용하기

#### 7.3.1 예제 컴포넌트 생성

LifeCycleSample.js 생성

```JS
import React, { Component } from "react";

class LifeCycleSample extends Component {
  state = {
    number: 0,
    color: null,
  }

  myRef = null; // ref를 설정할 부분

  constructor(props) {
    super(props);
    console.log('constructor')
  }

  // 컴포넌트가 최초 마운트될 때와 업데이트될 때 redder 호출 전에 호출     
  // 부모에게서 받은 color 값을 state에 동기화
  static getDerivedStateFromProps(nextProps, prevState) { 
    console.log('getDerivedStateFromProps');
    if(nextProps.color !== prevState.color) {
      return { color: nextProps.color };
    }
    return null;
  }

  // 컴포넌트를 만들고 첫 렌더링을 다 마친 후 실행 
  componentDidMount() {
    console.log('componentDidMount');
  }

  // props나 state를 변경했을 때 리렌더링을 시작할지 여부를 지정   
  shouldComponentUpdate(nextProps, nextState) {
    console.log('shouldComponentUpdate', nextProps, nextState);
    return nextState.number % 10 !==4; // 숫자의 마지막 자리가 4면 리렌더링하지 않음
  }

  // 컴포넌트가 DOM에서 제거되기 직전에 실행함
  componentWillUnmount() {
    console.log('componentWillUnmount');
  }

  handleClick = () => {
    this.setState({
      number: this.state.number + 1
    });
  }

  // 컴포넌트의 변화를 DOM에 반영하기 바로 직전에 호출하는 메서드
  // DOM에 변화가 일어나기 직전의 색상 속성을 snapshot값으로 반환해서 componentDidUpdate 에서 조회할 수 있게 함
  getSnapshotBeforeUpdate(prevProps, prevState) {
    console.log('getSnapshotBeforeUpdate');
    if(prevProps.color !== this.props.color) {
      return this.myRef.style.color;
    }
    return null;
  }

  // 컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드 최초 렌더링에서는 호출되지 않음
  componentDidUpdate(prevProps, prevState, snapShot) {
    console.log('componentDidUpdate', prevProps, prevState);
    if(snapShot) {
      console.log('업데이트되기 직전 색상: ', snapShot);
    }
  }

  // render(): 
  render() {
    console.log('render');

    const style = {
      color: this.props.color
    };

    return (
      <div>
        <h1 style={style} ref={ref => this.myRef=ref}>
          {this.state.number}
        </h1>
        <p>color: {this.state.color}</p>
        <button onClick={this.handleClick}>
          더하기
        </button>
      </div>
    )
  }
}

export default LifeCycleSample;
```

App.js
```JS
import React, { Component } from "react";
import LifeCycleSample from "./LifeCycleSample";

// 랜덤 색상을 생성
function getRandomColor() {
  return '#' + Math.floor(Math.random() * 16777215).toString(16);
}

class App extends Component {

  state = {
    color:'#000000'
  }

  handleClick = () => {
    this.setState({
      color: getRandomColor()
    })
  }

  render() {
    return (
      <div>
        {/* 버튼을 클릭할 때 마다 handleClick 호출 */}
        <button onClick={this.handleClick}>랜덤 색상</button>
        {/* color값을 props로 설정 */}
        <LifeCycleSample color={this.state.color} />
      </div>
    );
  }
}

export default App;
```

#### 7.3.3 에러 잡아내기

LifeCycleSample.js
```JS
render() {
  console.log('render');

  const style = {
    color: this.props.color
  };

  return (
    <div>
      {this.props.missing.value} // 존재하지 않은 props인 missing 객체의 value를 조회해서 오류 발생 시킴
      <h1 style={style} ref={ref => this.myRef=ref}>
        {this.state.number}
      </h1>
      <p>color: {this.state.color}</p>
      <button onClick={this.handleClick}>
        더하기
      </button>
    </div>
  )
}
```

ErrorBoundary.js 생성

```JS
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  state = {
    error: false
  };

  // 에러가 발생하면 componentDidCatch 호출
  componentDidCatch(error, info) {
    this.setState({
      error: true 
    });
    console.log({ error, info });
  }

  // render 함수는 this.state.error 값이 true일 때 에러 발생 문구를 보여줌
  render() {
    if (this.state.error) return <div>에러가 발생했습니다.</div>;
    return this.props.children;
  }
}

export default ErrorBoundary;
```

App.js

```JS
render() {
    return (
      <div>
        {/* 버튼을 클릭할 때 마다 handleClick 호출 */}
        <button onClick={this.handleClick}>랜덤 색상</button>
        <ErrorBoundary> // 감싸줌
          {/* color값을 props로 설정 */}
          <LifeCycleSample color={this.state.color} />
        </ErrorBoundary>
      </div>
    );
  }
```

### 7.4 정리

라이프사이클 도표   
<https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/>

라이프사이클 메서드는 컴포넌트 상태에 변화가 있을 때마다 실행하는 메서드   
서드파티 라이브러리를 사용하거나 DOM을 직접 건드려야 하는 상황에서 유용   
컴포넌트 업데이트 성능을 개선할 때는 shouldComponentUpdate가 중요하게 사용됨   


## 8장 Hooks

### 8.1 useState

CounterHook.js
```JS
import React, { useState } from 'react';

const CounterHook = () => {
  // useState 함수 파라미터에는 상태의 기본값(0)을 넣어줌
  // 즉 카운터의 기본값(value)을 0으로 설정하겠다는 의미
  const [value, setValue] = useState(0);
  // 배열의 첫 번째는 원소의 상태값, 두 번째 원소는 상태 설정 함수

  return(
    <div>
      <p>
         현재 카운터 값은 <b>{value}</b>입니다.
      </p>
      <button onClick={() => setValue(value + 1)}> +1</button>
      <button onClick={() => setValue(value - 1)}> -1</button>
    </div>
  );
};

export default CounterHook;
```

#### 8.1.1 useState를 여러 번 사용하기 

Info.js

```JS
import React,  { useState } from 'react';

const Info = () => {
  const [name, setName] = useState('');
  const [nickname, setNickname] = useState('');

  const onChangeName = e => {
    setName(e.target.value);
  };

  const onChangeNickname = e => {
    setNickname(e.target.value);
  };

  return(
    <div>
      <div>
        <input value={name} onChange={onChangeName} />
        <input value={nickname} onChange={onChangeNickname} />
      </div>

      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임:</b> {nickname}
        </div>
      </div>
    </div>
  )
} 

export default Info;
```


### 8.2 useEffet
리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook
클래스형 컴포넌트의 componentDidMount와 componentDidUpdate를 합친 형태

```JS
import React,  { useState, useEffect } from 'react';

const Info = () => {
  const [name, setName] = useState('');
  const [nickname, setNickname] = useState('');

  // 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행하도록 설정
  useEffect(() => {
    console.log('렌더링이 완료되었습니다!');
    console.log({
      name,
      nickname
    });
  });

  const onChangeName = e => {
    setName(e.target.value);
  };

  const onChangeNickname = e => {
    setNickname(e.target.value);
  };

  return(
    <div>
      <div>
        <input value={name} onChange={onChangeName} />
        <input value={nickname} onChange={onChangeNickname} />
      </div>

      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임:</b> {nickname}
        </div>
      </div>
    </div>
  )
} 

export default Info;
```

#### 8.2.1 마운트될 때만 실행하고 싶을 때

맨 처음 렌더링될 때만 실행하고 업데이트될 때는 실행하지 않으려면 함수의 두 번째 파라미터로 비어 있는 배열을 넣어 주면 됨

```JS
useEffect(() => {
  console.log('마운트될 때만 실행');
}, []); // 두 번째 파라미터로 비어 있는 배열을 넣어줌
```

#### 8.2.2 특정 값이 업데이트될 때만 실행하고 싶을 때 
useEffect의 두 번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값을 넣어줌

```JS
useEffect(() => {
  console.log(name);
}, [name]); // 두 번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값 설정
```

#### 8.2.3 뒷정리하기

useEffect는 기본적으로 렌더링되고 난 직후마다 실행되며 두 번째 파라미터 배열에 무엇을 넣는지에 따라 실행 조건이 달라짐   
컴포넌트가 언마운트되기 전이나 업데이트되기 직전에 어떠한 작업을 수행하고 싶다면   
useEffect에서 뒷정리(cleanup) 함수를 반환해 주어야함   
뒷정리 함수가 호출될 때는 업데이트되기 직전의 값을 보여 줌   
언마운트될 때만 뒷정리 함수를 호출하고 싶다면 useEffect 함수의 두 번째 파라미터에 빈 배열을 넣음   

```JS
useEffect(() => {
  console.log('effect');
  console.log(name);
    
  // 컴포넌트가 언마운트되기 전이나 업데이트되기 직전에 어떠한 작업을 수행하고 싶다면   
  // useEffect에서 뒷정리(cleanup) 함수를 반환해 주어야함 
  return () => {
    console.log('cleanup');
    console.log(name);
  };
}); // 언마운트 때만 뒷정리 함수를 호출하고 싶다면 두 번째 파라미터에 빈 배열을 넣음
```

### 8.3 useReducer
useReducer는 useState보다 더 다양한 컴포넌트 상황에 따라 더 다양한 상태를 다른 값으로 업데이트하고 싶을 때 사용하는 Hook   
리듀서는 현재 상태 그리고 업데이트를 위해 필요한 정보를 담은 액션 값을 전달받아 새로운 상태를 반환하는 함수   
리듀서 함수에서 새로운 상태를 만들 때는 반드시 불변성을 지켜주어야함   

```JS
function reducer(state, action) {
  return {...}; // 불변성을 지키면서 업데이트한 새로운 상태를 반환
}
```
액션 값은 주로 다음과 같은 형태 
```JS
{
  type: 'INCREMENT',
  // 다른 값들이 필요하다면 추가로 들어감
}
```

useReducer에서 사용하는 액션 객체는 반드시 type을 지니고 있을 필요가 없고 객체가 아니라 문자열, 숫자여도 상관 없음
useReducer의 가장 큰 장점은 컴포넌트 업데이트 로직을 컴포넌트 바깥으로 빼낼 수 있다는 것

8.3.1 카운터 구현하기

CounterHook.js

```JS
import React, { useReducer } from 'react';

function reducer(state, action) {

  // action.type에 따라 다른 작업 수행 
  switch (action.type) {
    case 'INCREMENT':
      return { value: state.value + 1 };
    case 'DECREMENT':
      return { value: state.value - 1 };
    default:
    
    // 아무것도 해당되지 않을 때 기존 상태 변환
    return state;
  }
}

const CounterHook = () => {
  // useReducer의 첫 번쨰 파라미터에는 리듀서 함수(reducer), 두 번째 파라미터에는 해당 리듀서의 기본 값({value: 0})을 넣음
  // 이 훅은 state(현재 가리키고 있는 상태) 값과 dispatch(액션을 발생시키는 함수) 함수를 받아옴
  const [state, dispatch] = useReducer(reducer, {value: 0});  

  return(
    <div>
      <p>
         현재 카운터 값은 <b>{state.value}</b>입니다.
      </p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}> +1</button> {/* dispatch(action) 형태로 함수 안에 파라미터로 액션 값을 넣어주면 리듀서 함수가 호출됨 */}
      <button onClick={() => dispatch({ type: 'DECREMENT' })}> -1</button>
    </div>
  );
};

export default CounterHook;
```

### 8.4 useMemo

useMemo를 사용하면 함수형 컴포넌트 내부에서 발생하는 연산을 최적화할 수 있음   

Average.js

```JS
import React, { useState, useMemo } from 'react';

const getAverage = numbers => {
  console.log('평균값 계산 중...');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');
  
  const onChange = e => {
      setNumber(e.target.value);
  }

  const onInsert = e => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber('');
  };

  const avg = useMemo(() => getAverage(list), [list]);
  // list 배열의 내용이 바뀔 때만 getAverage 함수 호출

  return(
    <div>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값:</b> {avg}
      </div>
    </div>
  );
};

export default Average;
```

### 8.5 useCallback

useMemo와 비슷한 함수   
주로 렌더링 성능을 최적화해야 하는 상황에서 사용   
이 Hook을 사용하면 이벤트 핸들러 함수를 필요할 때만 생성할 수 있음   
위의 Average.js는 컴포넌트가 리렌더링될 때마다 onChange, onInsert 함수들이 새로 생성됨   
컴포넌트의 렌더링이 자주 발생하거나 렌더링해야 할 컴포넌트의 개수가 많아지면 최적화를 해주는 것이 좋음      
첫 번째 파라미터에는 생성하고 싶은 함수, 두 번째 파라미터에는 배열.   
배열에는 어떤 값이 바뀌었을 때 함수를 새로 생성해야하는지 명시해야함   
빈 배열은 컴포넌트가 처음 렌더링될 때만 함수 생성   

함수 내부에서 상태 값에 의존해야 할 때는 그 값을 반드시 두 번쨰 파라미터 안에 포함시켜 주어야함   
onChange의 경우 기존의 값을 조회하지 않고 바로 설정만 하기 때문에 배열이 비어 있어도 상관 없지만   
onInsert는 기존의 number와 list를 조회해서 nextList를 생성하기 때문에 배열에 값을 꼭 넣어 주어야함

```JS
import React, { useState, useMemo, useCallback } from 'react';

const getAverage = numbers => {
  console.log('평균값 계산 중...');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');
  
  // useCallback: 첫 번째 파라미터에는 생성하고 싶은 함수, 두 번째 파라미터에는 배열
  const onChange = useCallback (e => { 
      setNumber(e.target.value);
  }, []); 
  // 빈 배열은 컴포넌트가 처음 렌더링될 때만 함수 생성
  // 기존 값을 조회하지 않고 바로 설정만 하기 때문에 빈 배열 가능
  
  const onInsert = useCallback(() => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber('');
  }, [number, list]); 
  // 배열의 number 혹은 list가 바뀌었을 때만 함수 생성

  const avg = useMemo(() => getAverage(list), [list]);
  // list 배열의 내용이 바뀔 때만 getAverage 함수 호출

  return(
    <div>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값:</b> {avg}
      </div>
    </div>
  );
};

export default Average;
```
useCallback은 useMemo로 함수를 반환하는 상황에서 더 편하게 사용할 수 있는 Hook   
숫자, 문자열, 객체처럼 일반 값을 재사용하려면 useMemo를 사용하고, 함수를 재사용하려면 useCallback를 사용 


```JS
useCallback(() => {
  console.log('hello world!');
}, [])

```

```JS
useMemo(() => {
  const fn = () => {
    console.log('hello world');
  };
  return fn;
}, [])
```

### 8.6 useRef

useRef Hook은 함수형 컴포넌트에서 ref를 쉽게 사용할 수 있도록 해줌   
useRef를 사용하여 ref를 설정하면 useRef를 통해 만든 객체 안의 current 값이 실제 엘리먼트를 가리킴   
다시 랜더링이 되더라도 기존에 참조하고 있던 컴포넌트 함수 내의 값이 그대로 보존되야 하는 경우에 사용   

useRef 함수는 current 속성을 가지고 있는 객체를 반환하는데, 인자로 넘어온 초기값을 current 속성에 할당함   
이 current 속성은 값을 변경해도 상태를 변경할 때 처럼 React 컴포넌트가 다시 랜더링되지 않음    
React 컴포넌트가 다시 랜더링될 때도 마찬가지로 이 current 속성의 값이 유실되지 않는다.   
<https://www.daleseo.com/react-hooks-use-ref/>   

Average.js

```JS
import React, { useState, useMemo, useCallback, useRef } from 'react';

const getAverage = numbers => {
  console.log('평균값 계산 중...');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');
  const inputEl = useRef(null);
  
  // useCallback: 첫 번째 파라미터에는 생성하고 싶은 함수, 두 번째 파라미터에는 배열
  const onChange = useCallback (e => { 
      setNumber(e.target.value);
  }, []); 
  // 빈 배열은 컴포넌트가 처음 렌더링될 때만 함수 생성
  // 기존 값을 조회하지 않고 바로 설정만 하기 때문에 빈 배열 가능
  
  const onInsert = useCallback(() => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber('');
      inputEl.current.focus(); // 등록 버튼을 눌렀을 때 포커스가 인풋으로 넘어어감
  }, [number, list]); 
  // 배열의 number 혹은 list가 바뀌었을 때만 함수 생성

  const avg = useMemo(() => getAverage(list), [list]);
  // list 배열의 내용이 바뀔 때만 getAverage 함수 호출

  return(
    <div>
      <input value={number} onChange={onChange} ref={inputEl} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값:</b> {avg}
      </div>
    </div>
  );
};

export default Average;
```

8.6.1 로컬 변수 사용하기 
컴포넌트 로컬 변수를 사용해야 할 때도 useRef를 활용할 수 있음   
로컬 변수란 렌더링과 상관없이 바뀔 수 있는 값을 의미   


클래스형 컴포넌트

```JS
import React, { Component } from 'react';

class MyComponent extends Component {
  id = 1
  setId = (n) => {
    this.id = n;
  }
  printId = () => {
    console.log(this.id);
  }
  render() {
    return (
      <div>
      	MyComponent
      </div>
    );
  }
}
export default Mycomponent;
```

함수형 컴포넌트 

```JS
import React, {useRef} from 'react';

const RefSample = () => {
  const id = useRef(1);
  const setId = (n) => {
    id.current = n;
  }
  const printId = () => {
    console.log(id.current);
  }
  return(
    <div>
      refsample
    </div>
  );
};

export default RefSample;
```
ref 안의 값이 바뀌어도 컴포넌트가 렌더링되지 않는다는 점에 주의해야함   
렌더링과 관련되지 않은 값을 관리할 때만 위 방식으로 작성


### 8.7 커스텀 Hooks 만들기
여러 컴포넌트에서 비슷한 기능을 공유할 경우, 이를 여러분만의 Hook으로 작성하여 로직을 재사용할 수 있음

useInputs.js

```JS
import { useReducer } from 'react'

function reducer(state, action) {
  return {
    ...state,
    [action.name]: action.value
  };
}

export default function useInputs(initialForm) {
  const [state, dispatch] = useReducer(reducer, initialForm);
  const onChange = e => {
    dispatch(e.target);
  };
  return [state, onChange];
}
```

Info.js
```JS
import React from 'react';
import useInputs from './useInputs';

const Info = () => {
  const [state, onChange] = useInputs({
    name: '',
    nickname: ''
  })
  const { name, nickname } = state;

  return(
    <div>
      <div>
        <input name="name" value={name} onChange={onChange} />
        <input name="nickname" value={nickname} onChange={onChange} />
      </div>

      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임:</b> {nickname}
        </div>
      </div>
    </div>
  )
} 

export default Info;
```


### 8.8 다른 Hooks

다른 개발자들이 만든 Hooks 

<https://nikgraf.github.io/react-hooks/>   
<https://github.com/rehooks/awesome-react-hooks>

### 8.9 정리
리액트에서 Hooks 패턴을 사용하면 클래스형 컴포넌트를 작성하지 않고도 대부분의 기능을 구현할 수 있음    
메뉴얼에서는 새로 작성하는 컴포넌트의 경우 함수형 컴포넌트와 Hooks를 사용할 것을 권장   


## 9장 컴포넌트 스타일링

스타일링 방식  
* 일반 css: 컴포넌트를 스타일링하는 가장 기본적인 방식
* Sass: 자주 사용되는 CSS 전처리기 중 하나로 확장된 CSS 문법을 사용하여 CSS 코드를 더욱 쉽게 작성할 수 있도록 해줌
* CSS Module: 스타일을 작성할 때 CSS 클래스가 다른 CSS 클래스의 이름과 절대 충돌하지 않도록 파일마다 고유한 이름을 자동으로 생성해주는 옵션
* styled-components: 스타일을 자바스크립트 파일에 내장시키는 방식으로 스타일을 작성함과 동시에 해당 스타일이 적용된 컴포넌트를 만들 수 있게 해줌

### 9.1 가장 흔한 방식, 일반 CSS

### 9.2 Sass 사용하기
별도의 추가 설정 없이 바로 사용 가능    
.sass와 .scss는 문법적 차이가 있음   
.sass는 {}와 ;을 사용하지 않음   

#### 9.2.1 utils 함수 분리하기
여러 파일에서 사용될 수 있는 Sass 변수 및 믹스인은 다른 파일로 분리하여 작성할 수 있음

#### 9.2.2 sass-loader 설정 커스터마이징하기
sass 파일을 상대경로를 절대경로로 불러오기 위해 사용

```bash
 yarn eject 
```
위 명령어 실행 후 질문에 y   
config 폴더내 webpack.config.js에서 수정


```JS
{
  test: sassRegex,
  exclude: sassModuleRegex,
  use: getStyleLoaders({
      importLoaders: 3,
      sourceMap: isEnvProduction
        ? shouldUseSourceMap
        : isEnvDevelopment,
      modules: {
        mode: 'icss',
      },
      // 'sass-loadeer' 삭제 후 아래 내용 추가
  
  }).concat({
    loader: require.resolve('sass-loader'),
    options: {
      includePaths: [paths.appSrc + 'styleds'],
      sourceMap: isEnvProduction
        ? shouldUseSourceMap
        : isEnvDevelopment,
      data: `@import 'utils';` // data 옵션은 sass 파일을 불러올 때 마다 코드 맨 윗부분에 특정 코드를 포함 시켜줌
    }
  }),
  
  sideEffects: true,
},
```

#### 9.2.3 node_modules에서 라이브러리 불러오기

```JS
@import '~library/styles';
```

### 9.3 CSS Module
css에서 사용할 클래스 이름을 고유한 값 파일이름_클래스이름_해시값 형태로 자동으로 만들어 컴포넌트 스타일 클래스 이름이 중첩되는 현상을 방지해 주는 기술   
리액트에서 .module.css 확장자로 파일을 저장하기만 하면 CSS Module 모듈 적용   
클래스를 적용하고 싶은 JSX 엘리먼트에 className={styles.클래스이름} 형태로 전달해주면 됨   
템플릿 리터럴을 사용하여 다중 클래스 지정 가능 

```JS
<div className={`${styles.클래스이름1} {styles.클래스이름2}`}> </div>
```
다음과 같이 작성할 수도 있음 

```JS
className={[styles.wrapper, styles.inverted].join('')}
```

#### 9.3.1 classnames
CSS 클래스를 조건부로 설정할 때 매우 유용한 라이브러리   


#### 9.3.2 Sass와 함께 사용하기
파일이름에 .module.scss 확장자를 사용해주면 사용가능

#### 9.3.3 CSS Module이 아닌 파일에서 CSS Module 사용하기

### 9.4 styled-component 
컴포넌트의 스타일링의 또 다른 패러다임인 CSS-in-JS (자바스크립트 파일 안에 스타일을 선언)   
이를 대체할 수 있는 라이브러리는 현재 emotions이 대표적 

StyledComponent.js
```JS
import React from 'react';
import styled, { css } from 'styled-components';


const Box = styled.div`
  /* props로 넣어 준 값을 직접 전달해 줄 수 있음 */
  background: ${props => props.color || 'blue'};
  padding: 1rem;
  display: flex;
`;

const Button = styled.button`
  background: white;
  color: black;
  border-radius: 4px;
  padding: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  font-size: 1rem;
  font-weight: 600;

  &:hover {
    background: rgba(255, 255, 255, 0.9);
  }
  
  ${props => 
    props.inverted &&
    css`
      background: none;
      border: 2px solid white;
      color: white;
      &:hover {
        background: white;
        color: black;
      }
    `};
    
  & + button {
      margin-left: 1rem;
  }
`;

const StyledComponent = () => (
  <Box color="black">
    <Button>안녕하세요</Button>
    <Button inverted={true}>테두리만</Button>
  </Box>
);

export default StyledComponent;
```
#### 9.4.1 Tagged 템플릿 리터럴
`(백틱)을 사용하는 문법을 Tagged 템플릿 리터럴이라고 부름   
일반 템플릿 리터럴과 다른 점은 템플릿 안에 자바스크립트 객체나 함수를 전달할 때 온전히 추출할 수 있음   

```JS
function tagged(...args) {
  console.log(args);
}
tagged`hello ${{ foo: 'bar' }} ${() => 'world'}!`
```

```JS
`ABC${value1}EFG${value2}HIJ${value3}`
// ABC, EFG, HIJ(,+ "")와 value1, value2, value3로 분해
```

#### 9.4.2 스타일링된 엘리먼트 만들기

예시
```JS
import styled from 'styled-components';
 
const MyComponent = styled.div`
  font-size: 2rem;
`;
```
사용해야 할 태그명이 유동적이거나 특정 컴포넌트 자체에 스타일링해 주고 싶다면 다음과 같이 구현
```JS
// 태그의 타입을 styled 함수의 인자로 전달
const MyInput = styled('input')`
  background: gray;
`
// 아예 컴포넌트 형식을 값에 넣어 줌
const StyledLink = styled(Link)` 
// 컴포넌트(Link)를 styled의 파라미터에 넣는 경우는 
// 해당 컴포넌트에 className props를 최상위 DOM의 className값으로 설정하는 작업이 내부적으로 되어 있어야함
  color: blue;
`
```

#### 9.4.3 스타일에서 props 조회하기
컴포넌트에 전달된 props값을 참조하여 스타일을 지정할 수 있음   

```JS
const Box = styled.div`
  // props로 넣어 준 값을 직접 전달해 줄 수 있음
  background: ${props => props.color || 'blue'};
  padding: 1rem;
  display: flex;
`;

// JSX에서 color값을 props로 넣어 줄 수 있음
<Box color="black">(...)</Box>
```
#### 9.4.4 props에 따른 조건부 스타일링
StyledComponent.js 에서 
```JS
  ${props => 
    props.inverted &&
    css`
      background: none;
      border: 2px solid white;
      color: white;
      &:hover {
        background: white;
        color: black;
      }
    `};
```

#### 9.4.5 반응형 디자인

 styled-components 매뉴얼에서 제공하는 유틸 함수를 사용
```JS
import React from 'react';
import styled, { css } from 'styled-components';
 
const sizes = {
  desktop: 1024,
  tablet: 768
};
 
// 위에 있는 size 객체에 따라 자동으로 media 쿼리 함수를 만들어 줌
// 참고: https://www.styled-components.com/docs/advanced#media-templates
const media = Object.keys(sizes).reduce((acc, label) => {
acc[label] = (...args) => css`
  @media (max-width: ${sizes[label] / 16}em) {
    ${css(...args)};
    }
`;
 
return acc;
}, {});
 
const Box = styled.div`
  /* props로 넣어 준 값을 직접 전달해 줄 수 있음 */
  background: ${props => props.color || 'blue'};
  padding: 1rem;
  display: flex;
  width: 1024px;
  margin: 0 auto;
  ${media.desktop`width: 768px;`}
  ${media.tablet`width: 100%;`};
`;
```
실제 사용한다면 별도의 파일로 모듈화해서 사용

### 9.5 정리



## 10장 일정 관리 웹 어플리케이션 만들기

### 10.1 프로젝트 준비하기
### 10.2 UI 구성하기
### 10.3 기능 구현하기
### 10.4 정리

## 11장 

