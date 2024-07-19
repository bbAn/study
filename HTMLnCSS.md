# HTML

## </> htmx   
<https://htmx.org/>   

## 11 HTML best practices for login & sign-up forms
<https://evilmartians.com/chronicles/html-best-practices-for-login-and-signup-forms>   


# CSS

## CSS Transform 분할   
CSS의 transform 속성은 모든 속성을 문자열로 나열해야 하기 때문에 수정이 번잡하고 어려웠다.   
이제 3개의 브라우저에서 모두 transform에 인라인으로 들어가던 속성들이 각각의 CSS 속성으로 지원된다.      

As-Is   
```CSS
.target:hover {
  transform: translateX(50%) rotate(30deg) scale(2);
}
```

To-Be
```CSS
.target:hover {
  translate: 50% 0;
  rotate: 30deg;
  scale: 2;
}
```
## The truth about CSS selector performance

브라우저 엔진은 웹 페이지 내 특정 영역에 대한 변화로 인해 새로운 DOM 트리가 업데이트되면,    
현재 페이지에 적용된 CSS stylesheet를 통해 스타일을 적용하며, 스타일과 DOM 트리를 매칭하는 것을 style recalculation이라 부른다.

이 튜토리얼은 Edge 개발자 도구(Chrome은 지원하지 않음)의 Performance(성능) 탭을 통해 대상 페이지를 프로파일링 한 후,    
Main 섹션에서 Recalculate Style 항목으로 수행된 작업에서 셀렉터들과 실행 시간(Selector Stats 결과 탭)을 확인해 볼 수 있는 방법을 설명한다.   

<https://blogs.windows.com/msedgedev/2023/01/17/the-truth-about-css-selector-performance/>

[참고] Analyze selector performance during Recalculate Style events   
<https://learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/evaluate-performance/selector-stats>



## Rem 그리고 Em, 언제 써야 할까   
<https://webdesign.tutsplus.com/ko/tutorials/comprehensive-guide-when-to-use-em-vs-rem--cms-23984>

## @property   
<https://developer.mozilla.org/en-US/docs/Web/CSS/@property>

## place-content
<https://developer.mozilla.org/en-US/docs/Web/CSS/place-content>

## How to Create CSS Conic Gradients for Pie Charts and More   
<https://www.sitepoint.com/create-css-conic-gradients-pie-charts/>   

## CSS inset   
<https://developer.mozilla.org/en-US/docs/Web/CSS/inset>   

## CSS inset-block   
<https://developer.mozilla.org/en-US/docs/Web/CSS/inset-block>   

## z-index: auto   

## CSS_Container_Queries   
<https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Container_Queries>    

## :indeterminate
<https://developer.mozilla.org/en-US/docs/Web/CSS/:indeterminate>

## :focus-visible
<https://hohoya33.tistory.com/93>   
<https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-visible>  

## :focus-within
<https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-within>
<https://developer.mozilla.org/ko/docs/Web/CSS/:focus-within>

## env
<https://developer.mozilla.org/en-US/docs/Web/CSS/env>

## backdrop-filter
<https://developer.mozilla.org/en-US/docs/Web/CSS/backdrop-filter>

## :placeholder-shown
<https://developer.mozilla.org/en-US/docs/Web/CSS/:placeholder-shown>

## clamp
<https://developer.mozilla.org/en-US/docs/Web/CSS/clamp>

## isolation
<https://developer.mozilla.org/en-US/docs/Web/CSS/isolation>

### Fluid Typography
<https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/>

## CSS container queries
<https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_container_queries>

## prefers-reduced-motion
<https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_container_queries>

## styled-components에서 props 사용하여 스타일값 지정하기
```TS

const PentagonContainer = styled.div<{ width?: number; height?: number }>`
  position: relative;
  width: ${({ width }) => width ?? 500}px; // ??은 width로 전달된 값이 없으면 기본적으로 500px로 지정
  height: ${({ height }) => height ?? 500}px;
`

export const IconButtonCommon = css<{ translucent?: boolean }>`
  display: inline-flex;
  align-items: center;
  justify-content: center;
  ${(props) => {
    const size = props.translucent ? "1.5625rem" : "2rem";
    return `
      width: ${size};
      height: ${size};
    `;
  }}
  
export const IconButtonGray = styled.button<{ translucent?: boolean }>`
  ${IconButtonCommon};
  background: ${(props) => props.translucent ? "rgba(0 0 0 / 0.3)" : colors.amsGray01};
`;


export const FilterItemStyle = styled.li<{
  isOn?: boolean;
  customText: string;
}>`
  width: ${(props) => (props.customText === "pF" ? "40%" : "60%")};
  height: 2rem;
  word-break: keep-all;

  * {
    vertical-align: middle;
  }
  ${(props) =>
    props.isOn &&
    css`
      ${FilterLink} {
        width: 100%;
        color: ${colors.white};
        background-color: #2c364e;
        border-radius: 100px;
        display: block;
        text-align: center;
        font-weight: 500;
        word-break: keep-all;
      }
    `}
`;


export const SideBar = styled.div<{ showAdvanceSearch: boolean }>`
  background-color: #e3e7ee;
  height: 100%;
  text-decoration: none;
  transition: 3s all ease-in-out;
  &.show-sidebar {
    ${(props) =>
      props.showAdvanceSearch == true
        ? css`
            width: 0;
            overflow: hidden;
          `
        : css`
            width: 100%;
            overflow: initial;
            transition: 3s all ease-in-out;
          `};
  }
`

export const InputCheckbox = styled.input.attrs({
  type: "checkbox",
})``;

export const InputRadio = styled.input.attrs({
  type: "radio",
})``;

```

## Inline conditionals in CSS?
<https://lea.verou.me/blog/2024/css-conditionals/>   
CSS WG은 24년 6월 회의에서 논의를 통해 인라인 if() 함수 문법 추가에 대한 합의를 이뤘다.   
합의가 이뤄지긴 했지만, 표준 명세에 도달하기 까지는 긴 과정(낙관적 관점에서도 2년여)이 예상된다.   
하지만 다양한 사용성을 제공할 수 있다는 측면에서 기대되는 명세다.   
명세에 대한 자세한 논의는 제안서를 통해 확인할 수 있다.  
