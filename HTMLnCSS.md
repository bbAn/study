# HTML





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

