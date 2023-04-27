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


## 클래스형 컴포넌트에서 input file과 버튼 연결하기 

```TS
class AssetSummaryCard extends Component<Props, State> {
  private fileInput: React.RefObject<HTMLInputElement>; // 1
  constructor(props: Readonly<Props>) {
        super(props);
        this.fileInput = React.createRef(); // 2
        this.state = {
           ...
        };
        this.handleUploadButtonClick = this.handleUploadButtonClick.bind(this); // 3
    }
    
    render() {
      private handleUploadButtonClick() { // 4
        this.fileInput.current?.click();
      }
      
      
      <>
        <IconButtonGray translucent
                        className="btn-upload"
                        aria-label="btn-upload"
                        onClick={this.handleUploadButtonClick} // 5
        />
        <input type="file"
               aria-label="input-image"
               ref={this.fileInput}  // 6
               onChange={async (e) => {
                   await this.handleAttachedFile(e)
               }}/>
      </>
    }
}
```

## JSON 데이터 값에서 특정부분 html 태그로 감싸기
```TS

  const dataTableScenario = [
    {
      id: "region_id",
      label: "Region",
      value: detailScenario.region,
    },
    {
      id: "factory",
      label: "Factory",
      value: detailScenario.factory,
    },
    {
      id: "substation",
      label: "Substation",
      value: detailScenario.substation,
    },
    {
      id: "assetsevaluated",
      label: "No. of Assets Evaluated",
      value: detailScenario.assetsevaluated,
    },
    {
      id: "oldest_asset",
      label: "Oldest Asset Age (yrs)",
      value: detailScenario.oldest_asset,
    },
    {
      id: "young_asset",
      label: "Youngest Asset Age (yrs)",
      value: detailScenario.young_asset,
    },
    {
      id: "real_life",
      label: "Real Life (yrs)",
      value: detailScenario.real_life,
    },
    {
      id: "standard_deviation",
      label: "Standard Deviation",
      value: detailScenario.standard_deviation,
    },
    {
      id: "rebuild_age",
      label: "Asset Rebuild Age (yrs)",
      value: detailScenario.rebuild_age,
    },

    //
    {
      id: "replacement_cost",
      label: "Replacement Cost ($)",
      value: detailScenario.replacement_cost,
    },
    {
      id: "rebuild_cost",
      label: "Rebuild Cost ($)",
      value: detailScenario.rebuild_cost,
    },
  ];
    
<TableInfo className="table-info">
  <tbody>
    {dataTableScenario.map(({ id, value, label }) => {
      const labelParts = label.split("("); // --- 첫 "("를 기준으로 문자열 분리
      return (
        <tr key={id}>
          <SubSubject widthTable="capital" scope="row">
            {labelParts[0]} <span> {labelParts.length > 1 && `(${labelParts[1]}`}</span>  // -- 분리된 문자열 적용
          </SubSubject>
          <FieldValue widthTable="capital" className="field-value">
            {listScenario.results.length > 0 ? value : ""}
          </FieldValue>
        </tr>
      );
    })}
    <tr>
      <SubSubject widthTable="capital" scope="row">
        <TitleWrap>
          <div className="text-left">Failure Probability Threshold</div>
          <div className="text-right">(%)</div>
        </TitleWrap>
      </SubSubject>
      <FieldValue widthTable="capital" className="field-value">
        {listScenario.results.length > 0
          ? detailScenario.pf_threshold
          : ""}
      </FieldValue>
    </tr>
  </tbody>
</TableInfo>

```


