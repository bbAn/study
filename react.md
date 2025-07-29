# React

## 1. 4 React Tips to Instantly Improve Your Code
<https://javascript.plainenglish.io/4-react-tips-to-instantly-improve-your-code-7456e028cfa3>

## 2. Next.js 제대로 알기   
<https://json.media/blog/proper_understading_of_nextjs>   

## 3. export의 방식 차이

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

## 4. 불변성

<https://hsp0418.tistory.com/171>


## 5. useState함수형 업데이트   

<https://velog.io/@tjdgus0528/React-Native-5x048oii>

## 6. Build Your Own React   
React를 처음부터 개발하는 과정을 다룸.   

원문 <https://pomb.us/build-your-own-react/>   
한글 번역 <https://bluewings.github.io/build-your-own-react/>

## 7. React의 구조와 JSX    
<https://gun-bro.tistory.com/4?category=911585>

## 8. [React.js]라우터   
<https://gun-bro.tistory.com/11>   
<https://gongbu-ing.tistory.com/45>   

## 9. history.push()로 페이지 이동시 props 넘겨주기
<https://velog.io/@dhlee91/this.props.history.push%EB%A1%9C-props-%EB%84%98%EA%B2%A8%EC%A3%BC%EA%B8%B0>   

## 10. [React] 로딩과 에러를 다루는 매뉴얼   
<https://10000cow.tistory.com/entry/React-%EB%A1%9C%EB%94%A9%EA%B3%BC-%EC%97%90%EB%9F%AC%EB%A5%BC-%EB%8B%A4%EB%A3%A8%EB%8A%94-%EB%A7%A4%EB%89%B4%EC%96%BC>   


## 11. 클래스형 컴포넌트에서 input file과 버튼 연결하기 

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

## 12. JSON 데이터 값 중 특정부분html 태그로 감싸기
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

## 13. 부모 컴포넌트에서 받은 props를 자식 컴포넌트 state에서 변경하고 다시 부모에게 넘겨주기
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

## 14. Redux를 사용해 헤더정보 가져오기

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

## 15. Redux 사용하기 
하위 컴포넌트인 GeneralChart에서 budget-button을 클릭했을 때 상위 컴포넌트인 ScenarioManagement의 ContentsWrapper하위에    
BudgetProposal 컴포넌트를 표시하도록 만들기 위해 Redux를 사용하여 상태를 관리하는 방법

### 1단계: Redux 설정
npm install @reduxjs/toolkit react-redux

### 2단계: 모달 상태 관리를 위한 Redux 슬라이스 생성
BudgetProposal 컴포넌트의 가시성을 관리할 새로운 Redux 슬라이스를 생성   

```TS
// src/redux/slices/modalSlice.js
import { createSlice } from '@reduxjs/toolkit';

export const modalSlice = createSlice({
  name: 'modal',
  initialState: {
    isBudgetProposalVisible: false,
  },
  reducers: {
    showBudgetProposal: (state) => {
      state.isBudgetProposalVisible = true;
    },
    hideBudgetProposal: (state) => {
      state.isBudgetProposalVisible = false;
    },
  },
});

export const { showBudgetProposal, hideBudgetProposal } = modalSlice.actions;

export default modalSlice.reducer;

```

### 3단계: 스토어에 슬라이스 추가
이 슬라이스를 Redux 스토어에 추가   

```TS
// src/redux/store.js
import { configureStore } from '@reduxjs/toolkit';
import modalReducer from './slices/modalSlice';

export const store = configureStore({
  reducer: {
    modal: modalReducer,
  },
});

export default store;

```

### 4단계: ScenarioManagement 컴포넌트에서 Redux 상태 사용
ScenarioManagement 컴포넌트를 수정하여 Redux 상태에 따라 BudgetProposal 컴포넌트를 조건부로 렌더링

```TS
// src/components/ScenarioManagement.js
import React from 'react';
import { useSelector } from 'react-redux';
import BudgetProposal from './scenarioDetail/BudgetProposal';

// 기타 import...

const ScenarioManagement = ({ theme }) => {
  // 기타 hooks 및 로직...

  const isBudgetProposalVisible = useSelector((state) => state.modal.isBudgetProposalVisible);

  return (
    <ContentsWrapper className="scenario-management overflow-hidden">
      {/* 기타 컴포넌트 및 로직... */}
      {isBudgetProposalVisible && (
        <BudgetProposal
          onCloseModal={() => setIsShowBudgetProposal(false)}
          scenarioId={selectedScenarioItem.objId}
          typeChart={typeChart}
        />
      )}
    </ContentsWrapper>
  );
};

export default withTheme(ScenarioManagement);

```

### 5단계: GeneralChart에서 모달 가시성 트리거
GeneralChart에서 budget-button 클릭 시 BudgetProposal을 보여주기 위해 Redux 액션을 디스패치

```TS
// src/components/GeneralChart.js
import React, { useMemo, useState } from 'react';
import { useDispatch } from 'react-redux';
import { showBudgetProposal } from '../../redux/slices/modalSlice'; // 경로에 맞게 수정
import { Button } from 'antd';
import HighchartsReact from 'highcharts-react-official';
import Highcharts from 'highcharts';

// 기타 import...

const GeneralChart = ({ theme, data, typeChart, scenarioId }) => {
  const dispatch = useDispatch();

  // 기타 hooks 및 로직...

  return (
    <ChartContainer style={{ height: '30rem' }}>
      {/* 기타 버튼 및 차트... */}
      <ButtonDefaultSmall
        className={"budget-button"}
        onClick={() => {
          dispatch(showBudgetProposal());
        }}
      >
        {getTranslationByKey("I18N_BUDGET_CHANGES")}
      </ButtonDefaultSmall>
    </ChartContainer>
  );
};

export default withTheme(GeneralChart);

```

### 6단계: Redux를 앱에 제공
앱의 메인 진입 파일에서 Redux provider로 애플리케이션 감쌈

```TS
// src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { store } from './redux/store';
import App from './App';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

### * store.ts 파일이 이미 존재하는 경우
modalSlice를 추가하여 기존의 설정에 통합하는 방식으로 진행

#### 1단계: modalSlice 추가

```TS
// src/redux/slices/modalSlice.ts
import { createSlice } from '@reduxjs/toolkit';

export const modalSlice = createSlice({
  name: 'modal',
  initialState: {
    isBudgetProposalVisible: false,
  },
  reducers: {
    showBudgetProposal: (state) => {
      state.isBudgetProposalVisible = true;
    },
    hideBudgetProposal: (state) => {
      state.isBudgetProposalVisible = false;
    },
  },
});

export const { showBudgetProposal, hideBudgetProposal } = modalSlice.actions;

export default modalSlice.reducer;
```

#### 2단계: store.ts 파일에 modalSlice 통합
store.ts 파일에 modalSlice를 통합   
기존의 rootReducer에 새로운 modal 리듀서를 추가   

```TS
import { configureStore, ThunkAction, Action } from "@reduxjs/toolkit";
import thunk from "redux-thunk";
import { combineReducers, applyMiddleware, createStore } from "redux";
import headerReducer, { LevelState } from "../modules/header/header.reducer";
import userReducer, { UserInfo } from "../modules/user/user.reducers";
import layoutReducer, { LayoutState } from "../modules/layoutState/layout.reducers";
import modalReducer from "../redux/slices/modalSlice";  // 새로운 slice를 import

const rootReducer = combineReducers({
    header: headerReducer,
    users: userReducer,
    layout: layoutReducer,
    modal: modalReducer,  // 여기에서 modal 리듀서를 추가
});

const store = createStore(rootReducer, applyMiddleware(thunk));

export default store;

// Infer the `RootState` and `AppDispatch` types from the store itself
export type RootState = {
    header: LevelState;
    users?: UserInfo;
    layout?: LayoutState;
    modal: ReturnType<typeof modalReducer>;  // RootState 타입에 modal 추가
}

// Inferred type: {posts: PostsState, comments: CommentsState, users: UsersState}
export type AppDispatch = typeof store.dispatch;
export type AppThunk<ReturnType = void> = ThunkAction<
    ReturnType,
    RootState,
    unknown,
    Action<string>
>;
```

#### 3단계: ScenarioManagement에서 Redux 상태 사용c
Redux 상태를 활용하여 ScenarioManagement 컴포넌트에서 BudgetProposal 컴포넌트를 표시할 수 있도록 변경

```TS
// src/components/ScenarioManagement.tsx
import React from 'react';
import { useSelector } from 'react-redux';
import { RootState } from '../redux/store';  // RootState 타입 import
import BudgetProposal from './scenarioDetail/BudgetProposal';

// 기타 import...

const ScenarioManagement = ({ theme }) => {
  // 기타 hooks 및 로직...

  const isBudgetProposalVisible = useSelector((state: RootState) => state.modal.isBudgetProposalVisible);

  return (
    <ContentsWrapper className="scenario-management overflow-hidden">
      {/* 기타 컴포넌트 및 로직... */}
      {isBudgetProposalVisible && (
        <BudgetProposal
          onCloseModal={() => setIsShowBudgetProposal(false)}
          scenarioId={selectedScenarioItem.objId}
          typeChart={typeChart}
        />
      )}
    </ContentsWrapper>
  );
};

export default withTheme(ScenarioManagement);
```

#### 4단계: GeneralChart에서 Redux 상태 변경 트리거
GeneralChart에서 budget-button 클릭 시 showBudgetProposal 액션을 디스패치하여 BudgetProposal을 표시

```TS
// src/components/GeneralChart.tsx
import React, { useMemo, useState } from 'react';
import { useDispatch } from 'react-redux';
import { showBudgetProposal } from '../redux/slices/modalSlice';  // 액션 가져오기
import { Button } from 'antd';
import HighchartsReact from 'highcharts-react-official';
import Highcharts from 'highcharts';

// 기타 import...

const GeneralChart = ({ theme, data, typeChart, scenarioId }) => {
  const dispatch = useDispatch();

  // 기타 hooks 및 로직...

  return (
    <ChartContainer style={{ height: '30rem' }}>
      {/* 기타 버튼 및 차트... */}
      <ButtonDefaultSmall
        className={"budget-button"}
        onClick={() => {
          dispatch(showBudgetProposal());  // 버튼 클릭 시 액션 디스패치
        }}
      >
        {getTranslationByKey("I18N_BUDGET_CHANGES")}
      </ButtonDefaultSmall>
    </ChartContainer>
  );
};

export default withTheme(GeneralChart);
```

## 16. React에서 Icon 다루기 with Typescript
<https://blog.toycrane.xyz/react%EC%97%90%EC%84%9C-icon-%EB%8B%A4%EB%A3%A8%EA%B8%B0-59b6d987d61f>   

## 17. JavaScript의 Object를 Map으로 변환

```TS
class CofInformation extends Component<Props, State> {
    constructor(props: Readonly<Props>) {
        super(props);

        this.state = {
            cofParameters: new Map() // 초기값을 빈 Map으로 설정
        }
    }

    private async refresh() {
        const {dashboardRepository, selectedAsset} = this.props;
        if (!selectedAsset.asset_id) return;

        const cofParametersObject = await dashboardRepository.getCofParameters(selectedAsset.asset_id);
        
        // Object를 Map으로 변환
        const cofParametersMap = new Map(Object.entries(cofParametersObject));

        this.setState({
            cofParameters: cofParametersMap
        });
    }
}
```

Object.entries(cofParametersObject)는 주어진 객체의 [key, value] 쌍을 배열로 반환함   
new Map()은 이 배열을 입력으로 받아 Map을 생성    
이렇게 하면 객체가 Map으로 변환되어 상태에 저장

## 18. 현재 선택된 target 외 클릭시 상태 변경 

```TS
// 함수형

  const dropdownRef = useRef<any>(null);
  const imgRef = useRef<HTMLImageElement>(null);

  useEffect(() => {
    const handleOutsideClick = (event: MouseEvent) => {
      if (
        dropdownRef.current &&
        !dropdownRef.current.contains(event.target as Node) &&
        imgRef.current !== event.target
      ) {
        setShowNotiList(false);
      }
    };
    document.addEventListener("mouseup", handleOutsideClick);
    return () => {
      document.removeEventListener("mouseup", handleOutsideClick);
    };
  }, []);

  const notificationList = () => {
    return (
      <NotificationList ref={dropdownRef}> // dropdownRef
        <Row justify="space-between" align="middle" className="p-4">
          <div className="noti-container-title">
            Unacknowledged Metric Messages
          </div>
          <Button className="all-history-btn" type="link">
            All History
            <RightOutlined color={blue17} />
          </Button>
        </Row>
        {notifications.map((noti) => (
          <Row className="noti-cell p-4">
            <Col span={17}>{noti.message}</Col>
            <Col span={7} className="noti-date">
              {noti.timestamp}
            </Col>
          </Row>
        ))}
      </NotificationList>
    );
  };

  const handleClick = () => {
    setShowNotiList((prevState) => !prevState);
  };

  return (
    <>
      <Badge count={notifications.length} size="small" offset={[-2, 5]}>
        <img
          className="cursor-pointer"
          src={SVGImages.ams.common.iconNotification()}
          alt="Notification"
          onClick={handleClick}
          ref={imgRef} //imgRef
        />
      </Badge>

      {showNotiList && notificationList()}
    </>
  );

```

```TS
// 클래스형

class YourComponent extends React.Component {
  public or private dropdownRef: React.RefObject<any>;
  public or private imgRef: React.RefObject<HTMLImageElement>;
  
  constructor(props: any) {
    super(props);
    this.state = {
      showNotiList: false
    };
    this.dropdownRef = React.createRef();
    this.imgRef = React.createRef();
  }

  componentDidMount() {
    document.addEventListener("mouseup", this.handleOutsideClick);
  }

  componentWillUnmount() {
    document.removeEventListener("mouseup", this.handleOutsideClick);
  }

  handleOutsideClick = (event: MouseEvent) => {
    if (
      this.dropdownRef.current &&
      !this.dropdownRef.current.contains(event.target as Node) &&
      this.imgRef.current !== event.target
    ) {
      this.setState({ showNotiList: false });
    }
  };

  private notificationList() {
    return (
      <NotificationList ref={dropdownRef}> // dropdownRef
        <Row justify="space-between" align="middle" className="p-4">
          <div className="noti-container-title">
            Unacknowledged Metric Messages
          </div>
          <Button className="all-history-btn" type="link">
            All History
            <RightOutlined color={blue17} />
          </Button>
        </Row>
        {notifications.map((noti) => (
          <Row className="noti-cell p-4">
            <Col span={17}>{noti.message}</Col>
            <Col span={7} className="noti-date">
              {noti.timestamp}
            </Col>
          </Row>
        ))}
      </NotificationList>
    );
  };

  render() {
    <>
      <Badge count={notifications.length} size="small" offset={[-2, 5]}>
        <img
          className="cursor-pointer"
          src={SVGImages.ams.common.iconNotification()}
          alt="Notification"
          onClick={handleClick}
          ref={this.imgRef} //imgRef
        />
      </Badge>

      {showNotiList && notificationList()}
    </>
  }
}
```

## 19. ResizableTable 넓이 변경 시 다른 셀 너비는 변경되지 않고 테이블 전체 넓이가 넓어지도록

```TS
// ListUser.tsx

const ListUser = ({setSelectedKeys, theme, userData, onReload}: Props) => {
  const [activeRowKey, setActiveRowKey] = useState("");
  const [totalColumnWidth, setTotalColumnWidth] = useState(2000);
  const selectedRowKey = useRef("");

  const onColumnResize = (newWidth: number) => {
      setTotalColumnWidth((prevWidth) => prevWidth + newWidth);
  };

  const rowSelection: TableRowSelection<Account> = {
      selectedRowKeys,
      onChange: onSelectChange,
      getCheckboxProps: (record: any) => {
          return {
              disabled: record.accountId === currentUserId,
              name: record.role,
          };
      },
  };

  const handleRowClick = (record: any, e: React.MouseEvent<HTMLTableRowElement>) => {
      record.editable = !record.editable;
      selectedRowKey.current = record.accountId;

      // e.target을 Element로 타입 선언하여 closest 메서드 사용 가능하게 함
      const target = e.target as Element; // 또는 HTMLElement로 선언.

      // 클릭된 요소와 가장 가까운 체크박스 또는 .ant-checkbox-inner 요소를 찾음.
      const isCheckboxClick = target.closest('.ant-checkbox-wrapper, .ant-checkbox, .ant-checkbox-inner, input[type="checkbox"]');

      // 체크박스 클릭 또는 이미 선택된 행을 클릭한 경우, 아무것도 하지 않음.
      if (isCheckboxClick || activeRowKey === record.accountId) {
          return;
      }

      // 그렇지 않은 경우, activeRowKey를 업데이트하여 배경색 변경.
      setActiveRowKey(record.accountId);
  };

  return (
    <ResizableTable
        rowKey="accountId"
        rowSelection={rowSelection}
        rowClassName={(record) =>
            record.accountId === activeRowKey ? "is-selected" : ""
        }
        dataSource={displayedUserData}
        columns={columns}
        onRow={(record) => ({
            onClick: (e) => handleRowClick(record, e),
        })}
        onColumnResize={onColumnResize}
        pagination={false}
        onChange={onChange}
        scroll={{x: totalColumnWidth, y: "71vh"}}
        expandable={{
            childrenColumnName: "invitedAccounts",
            expandIcon: ({expanded, onExpand, record}) => {
                return record.invitedAccounts ? (
                    <img src={theme.getImage(SVGImages.ams.common.iconExpanded)}
                         className={expanded ? "is-expanded" : ""}
                         onClick={(e) => {
                             e.stopPropagation();
                             onExpand(record, e);
                         }}
                         alt={expanded ? "collapse" : "expand"}
                    />
                ) : null;
            },
        }}
        excludedColumnKeys={["action"]}
    />
  )

}

```

```TS
// ResizableTable.tsx

const ResizableTitle = (
    props: React.HTMLAttributes<any> & {
        isResizable: boolean;
        onResize: (
            e: React.SyntheticEvent<Element>,
            data: ResizeCallbackData
        ) => void;
        width: number;
    }
) => {
    const {onResize, width, isResizable, ...restProps} = props;

    if (!width || !isResizable) {
        return <th {...restProps} />;
    }

    return (
        <Resizable
            width={width}
            height={0}
            handle={
                <ResizableColumnHandler
                    onClick={(e) => {
                        e.stopPropagation();
                    }}
                />
            }
            onResize={onResize}
            draggableOpts={{enableUserSelectHack: false}}
        >
            <th {...restProps} />
        </Resizable>
    );
};

const ResizableTable = ({
                            columns = [],
                            excludedColumnKeys = [],
                            columnMinWidth = 75,
                            onColumnResize, // 새로운 prop 추가
                            ...restProps
                        }: TableProps<any> & {
    excludedColumnKeys?: string[];
    columnMinWidth?: number;
    onColumnResize?: (newWidth: number) => void;
}) => {
    const [columnData, setColumnData] = useState<ColumnsType<any>>(
        columns.map((c) => ({...c, ellipsis: true}))
    );

    const handleResize = (index: number) => (
        _e: React.SyntheticEvent<Element, Event>, // 타입을 명시적으로 추가
        {size}: ResizeCallbackData
    ) => {
        const newSizeWidth = Number(size.width);
        if (newSizeWidth < columnMinWidth) return;

        setColumnData((prevColumns) => {
            const nextColumns = [...prevColumns];
            const currentWidth = nextColumns[index].width ? Number(nextColumns[index].width) : columnMinWidth;
            const deltaWidth = newSizeWidth - currentWidth; // 빼기 연산의 양변을 명시적으로 숫자로 처리
            nextColumns[index] = {
                ...nextColumns[index],
                width: newSizeWidth,
            };
            if (onColumnResize) onColumnResize(deltaWidth); // 너비 변경 시 콜백 호출
            return nextColumns;
        });
    };

    const resizableColumns: any[] = columnData.map((col, index) => ({
        ...col,
        onHeaderCell: (column: ColumnType<any>) => ({
            isResizable: !excludedColumnKeys.includes(column.key?.toString() ?? ""),
            width: column.width || columnMinWidth,
            onResize: handleResize(index),
        }),
    }));

    return (
        <Table
            {...restProps}
            columns={resizableColumns}
            components={{
                header: {
                    cell: ResizableTitle,
                },
            }}
        />
    );
};

export default ResizableTable;

```

## 20. 말줄임 여부 확인해서 툴팁(antd) 적용

```TS
  const EllipsisTooltip = ({ content }: { content: string }) => {
    const textRef = useRef<HTMLDivElement>(null);
    const [isEllipsis, setIsEllipsis] = useState(false);

    useEffect(() => {
      if (textRef.current) {
        setIsEllipsis(textRef.current.scrollWidth > textRef.current.clientWidth);
      }
    }, [content]);

    return (
      <Tooltip title={isEllipsis ? content : null} placement="topLeft">
        <div
          ref={textRef}
          style={{
            whiteSpace: "nowrap",
            overflow: "hidden",
            textOverflow: "ellipsis",
          }}
        >
          {content}
        </div>
      </Tooltip>
    );
  };

...

 <EllipsisTooltip content={} />

```


## 30.
```TS
    const handleRowClick = (record: any, e: React.MouseEvent<HTMLTableRowElement>) => {
        // e.target을 Element로 타입 선언하여 closest 메서드 사용 가능하게 함
        const target = e.target as Element; // 또는 HTMLElement로 선언해도 괜찮습니다.

        // 클릭된 요소와 가장 가까운 체크박스 또는 .ant-checkbox-inner 요소를 찾습니다.
        const isCheckboxClick = target.closest('.ant-checkbox-wrapper, .ant-checkbox, .ant-checkbox-inner, input[type="checkbox"]');

        // 체크박스 클릭 또는 이미 선택된 행을 클릭한 경우, 아무것도 하지 않습니다.
        if (isCheckboxClick || activeRowKey === record.accountId) {
            return;
        }

        // 그렇지 않은 경우, activeRowKey를 업데이트하여 배경색을 변경합니다.
        setActiveRowKey(record.accountId);
    };
```

## 31. 
```TS
<span dangerouslySetInnerHTML={{__html: svgContent}}>
```

## 32. 한글 입력 후 Enter시 메세지가 한 번 더 보내지는 이유
<https://velog.io/@jackson5272/%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EA%B8%B0-%ED%95%9C%EA%B8%80-%EC%9E%85%EB%A0%A5-%ED%9B%84-Enter%EC%8B%9C-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EA%B0%80-%ED%95%9C-%EB%B2%88-%EB%8D%94-%EB%B3%B4%EB%82%B4%EC%A7%80%EB%8A%94-%EC%9D%B4%EC%9C%A0>

## 33. React Query(Tanstack Query)
<https://tanstack.com/query/v4?from=reactQueryV3&original=https%3A%2F%2Freact-query-v3.tanstack.com%2F>
