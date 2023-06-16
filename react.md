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

## JSON 데이터 값 중 특정부분html 태그로 감싸기
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

## 부모 컴포넌트에서 받은 props를 자식 컴포넌트 state에서 변경하고 다시 부모에게 넘겨주기
부모 컴포넌트의 특정 영역을 클릭 했을 때의 상태를 자식 컴포넌트의 props로 넘겨   
자식 컴포넌트에서 처리하는 state를 적용시킨 후 다시 부모 컴포넌트로 전달하는 방식   

### 부모 컴포넌트

```TS
import React, { Component } from 'react';


// 부모 컴포넌트는 isClearOverlay라는 상태를 가지고 있으며, 
// 초기값은 false 
// 이 상태는 자식 컴포넌트에게 넘겨주는 prop으로 사용됨

interface State {
  isClearOverlay: boolean;
}

class ParentComponent extends Component<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = {
      isClearOverlay: false,
    };
  }

  // handleChildState라는 함수를 통해 자식 컴포넌트로부터 상태를 받아와 부모의 상태를 업데이트. 
  // 이 함수는 자식 컴포넌트에게 callback으로 제공됨
  handleChildState = (clearOverlay: boolean) => {
    this.setState({ isClearOverlay: clearOverlay });
    // console.log("자식에서 받아온 state", this.state.isClearOverlay)
  }

  render() {
    return <div onClick={(e)=> {
              
              // 현재 클릭된 target에 특정 클래스 이름이 포함되어 있는지를 확인하고, 그에 따라 isClearOverlay 상태를 업데이트 
              const element = e.target as Element; // 현재 선택된 target. 리액트에서는 as Element를 사용해야함
              const classNames = ["heatmap-point", "overlay", "text-link"];
              
              // some: 배열 메서드 
              // 배열의 각 요소에 대해 제공된 함수를 실행 
              // 함수가 한 번이라도 true를 반환하면, some 메서드는 true를 즉시 반환하고 더 이상 실행하지 않음
              const containsClass = classNames.some(name => element.classList.contains(name));
              

              this.setState({
                isClearOverlay: !containsClass,
                isShowAssetSubstation: containsClass
                })
              }}
            >
      // ChildComponent를 렌더링하고, isClearOverlay 상태와 handleChildState 함수를 prop으로 넘겨줌.
      <ChildComponent isClearOverlay={this.state.isClearOverlay} // 자식에게 넘겨주는 props
                      callback={this.handleChildState} // 자식에게 넘겨주는 함수
      />
    </div>
  }
}
```


### 자식 컴포넌트   

```TS
import React, { Component } from 'react';

// 부모 컴포넌트로부터 isClearOverlay 상태와 callback 함수를 prop으로 받아옴
interface Props {
  isClearOverlay?: boolean; 
  callback?: (clearOverlay: boolean) => void;
}

// clearOverlay 상태를 가지고 있으며, 
// 부모 컴포넌트로부터 받아온 callback 함수를 사용해 이 상태를 부모 컴포넌트에게 전달
interface State {
  clearOverlay: boolean;
}

class ChildComponent extends Component<Props, State> {
  constructor(props) {
    super(props);
    this.state = {
      clearOverlay: false,
    };
  }

  render() {
    const {clearOverlay} = this.state;
    const {callback} = this.props;

    {dataHeatMap?.length > 0 &&
    dataHeatMap?.map((data, index) => {
      return (
          <tr key={\`_${index}_${Math.random()}\`}>
            <td key={\`ab_${index}_${Math.random()}\`}>
              {data.criticality_range}
            </td>
            {data.pof.map((detail, idx) => {
              const mapping = {
                assetCount: detail.val,
                criticality: dataCoF[idx],
                failureProbability: data.criticality_range,
              };
              // customBackground.cof가 idx와 같고 customBackground.pof가 index와 같거나,
              // customBackground.cof가 빈 문자열인 경우, customClass는 "" (빈 문자열).
              // 그 외의 경우, customClass는 "active"
              const customClass =
                  (customBackground.cof === idx &&
                      customBackground.pof === index) ||
                  customBackground.cof === "" || this.props.isClearOverlay // 부모로부터 받은 isClearOverlay prop에 따라 "active"가 추가되거나 제거
                      ? ""
                      : "active";
              const coordinates = {
                cof: idx,
                pof: index,
              };

              return (
                  <PointStyle
                      key=index
                      bgColor={detail.color}
                      hasValue={!!detail.val}
                      className="heatmap-point"
                      onClick={() => {
                        this.setState(
                            {
                              customBackground: !detail.val // 값이 없으면
                                  ? {
                                    cof: "",
                                    pof: "",
                                  }
                                  : coordinates,
                              clearOverlay: !detail.val,
                            }, () => {}
                        );
                        
                        // 부모에게서 받은 callback props가 있으면 callback 함수에 clearOverlay값을 인자로 넘겨줌
                        callback && callback(clearOverlay); 
                      }}
                  >
                    <div className={\`overlay ${customClass}\`}>
                      <Link
                          className={"text-link"}
                          to={{
                            pathname: "/risk-matrix",
                          }}
                      >
                        {detail.val}
                      </Link>
                    </div>
                  </PointStyle>
              );
            })}
          </tr>
      );
    })}
  }
}

```

## Redux를 사용해 헤더정보 가져오기

클래스형 컴포넌트로 작성된 Header에서 Redux props로 제공해 하위 컴포넌트에서 정보를 확인하는 방법   
인데 Redux관련 다른 설정이 필요한데 우선 내가 사용했던 내용 위주로 정리

### Header 
header와 관련된 Redux 설정이 더 있으나 아직은 모르는 부분이라...      

```TS
import React, {Component} from "react";
import {connect} from "react-redux";
import {RootState} from "../app/store";

interface Props extends RootState {
...
}

export const TOP_NAV_ITEMS = {
  MAIN: "main",
  REGION: "region",
  FACTORY: "factory",
  SUBSTATION: "substation",
  ASSET: "asset",
};

class Header extends Component<Props, State> {
  render() {
    const { header: LevelState } = this.props;

    return (
      <div>
        <Header/>
      </div>
    );
  }
}

const mapStateToProps = (state: RootState) => ({
  header: state.header,
});

export default connect(mapStateToProps)(Header);
```

### 하위 컴포넌트
```TS
import React, {Component} from "react";
import {RootState} from "../app/store";
import {connect} from "react-redux";
import {TOP_NAV_ITEMS} from "../header/HeaderAMS";

interface Props extends RootState { // RootState를 사용해야 헤더에서 넘겨주는 header props를 받아 사용할 수 있음
...
}

class ChildComponent extends Component<Props, State> {
  render() {
    const {header} = this.props;
    return (
      <ChildContainer withHierarchy={header.level != TOP_NAV_ITEMS.MAIN}>
        {this.renderMainControll()}
        {this.renderHighCharts()}
      </ChildContainer>
    );
  }
}

const mapStateToProps = (state: RootState) => {
  return {
    header: state.header
  };
}

export default withRouter(
    withTheme(connect(mapStateToProps)(ChildComponent))
);
```

## React에서 Icon 다루기 with Typescript
<https://blog.toycrane.xyz/react%EC%97%90%EC%84%9C-icon-%EB%8B%A4%EB%A3%A8%EA%B8%B0-59b6d987d61f>   



