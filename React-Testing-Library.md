# React Testing Library (RTL)

React 컴포넌트를 테스트 하기 위해 만들어진 도구. 기본적으로 CRA에 내장되어 있으며 직접 환경 설정 가능   
Jest와 상호 보완 관계 (RTL이 Jest를 포함하는 구조)   
Jest를 통해 기능 테스트를 진행할 수 있지만 React의 컴포넌트를 렌더링하고 테스트하기 위해서 몇가지 기능이 더 필요함   

* Jest - 자체적인 test runner와 test util 제공
* RTL - Jest + React 컴포넌트 test util 제공

test runner는 테스트 실행 시 .test.js 를 가진 파일을 자동으로 탐색하며 테스트를 진행함   

* describe - 같은 맥락의 테스트들을 그룹화함
* it - 개별 테스트를 수행. test 메서드와 동일
* render - 테스트를 위해 특정 컴포넌트를 jsdom에 렌더링

테스트의 패턴은 대개 다음과 같다
1. 컴포넌트 띄우기
2. 특정 액션을 발생 시키기
3. 결과 확인

## Query
렌더링 된 DOM 노드에 접근하여 엘리먼트를 가져오는 메서드   

getAllByText의 예   

get(쿼리타입) / All(타켓의 갯수) / ByText(타겟 유형)   

쿼리타입   
* get - 동기적으로 처리되며 타켓을 찾지 못할 시 에러
* find - 비동기적으로 처리되며 타겟을 찾지 못할 시 에러
* query - 동기적으로 처리되며 타겟을 찾지 못할시 null 반환


타겟의 갯수   
* All - 다수의 엘리먼트가 탐색되는 상황

타겟 유형 (우선 순위 별 나열)

* ByRole
* ByLabelText
* ByPlaceholderText
* ByText
* ByDisplayValue
* ByAltText
* ByTitle
* ByTestId

```JS
// 두 쿼리는 모두 같은 element 탐색 (문자열 대신 정규식 탐색도 가능)
screen.getByRole('button', { name: '+' });
screen.getByText('+');
```

## Action
사용자가 브라우저에서 이벤트를 발생시키는 것처럼 타겟을 이용해 이벤트를 호출

```JS
const target = screen.getByRole('button', { name: '+' });
// fireEvent, userEvent api 모두 이벤트 호출 용도로 사용됨
fireEvent.click(target);
userEvent.click(target); //userEvent를 사용할 것을 권장
```

## Assertion
요소를 렌더링하고 타겟을 얻어 특정 이벤트를 실행하면 특정 결과가 발생함
이때 expect 메서드에 타겟을 인자로 넘겨 사용할 수 있음

```JS
const target = screen.getByRole('button', { name: '+' });
userEvent.click(target);
expect(screen.getByText('1')).toBeTruthy();
```









