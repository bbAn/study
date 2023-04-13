# React

## export의 방식 차이

```JS
// 단순 export
export const ExportComponentA = () => {}

export const ExportComponentB = () => {}

// 기본 export
export default ExportComponent;
```

* 단순 export
함수나 변수 앞에 export를 붙여줌

* 기본 export
default를 사용한 문법    
해당 모듈(현재 파일)에서 함수나 변수를 기본으로 내보겠다는 것   
import 할 때 {} 없이 import가 가능하며 아무이름으로나 import할 수 있음  
한개의 파일에서 내보내는 것은 하나이기 때문    

```JS
// 단순 export를 import
import {ExportComponentA, ExportComponentB} from "./ExportComponent"

// 기본 export import
import ExportComponent from "./ExportComponent.js"

```

## 불변성

<https://hsp0418.tistory.com/171>


## useState함수형 업데이트   

<https://velog.io/@tjdgus0528/React-Native-5x048oii>

## Build Your Own React   
React를 처음부터 개발하는 과정을 다룸.   

원문 <https://pomb.us/build-your-own-react/>   
한글 번역 <https://bluewings.github.io/build-your-own-react/>

## React의 구조와 JSX    
<https://gun-bro.tistory.com/4?category=911585>

## [React.js]라우터   
<https://gun-bro.tistory.com/11>   
<https://gongbu-ing.tistory.com/45>   

## history.push()로 페이지 이동시 props 넘겨주기
<https://velog.io/@dhlee91/this.props.history.push%EB%A1%9C-props-%EB%84%98%EA%B2%A8%EC%A3%BC%EA%B8%B0>   

## [React] 로딩과 에러를 다루는 매뉴얼   
<https://10000cow.tistory.com/entry/React-%EB%A1%9C%EB%94%A9%EA%B3%BC-%EC%97%90%EB%9F%AC%EB%A5%BC-%EB%8B%A4%EB%A3%A8%EB%8A%94-%EB%A7%A4%EB%89%B4%EC%96%BC>   




