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
