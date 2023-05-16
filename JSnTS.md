# JS

## sort()
sort함수는 사용하면 원본도 바꾸기 때문에    
원본은 유지하고 변수에만 정렬해서 가지고 싶다면 '비구조화 할당(destucturing assignment)' 표현식을 사용해야함   

* 구조분해 할당   
<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment>

* Spread syntax (...)   
<https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax>  


## .some()
배열 메서드   
배열 내의 항목 중 특정 조건에 해당하는 것이 하나라도 존재하는지 확인      

<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/some> 


## .every()
배열 메서드   
배열 내의 모든 항목이 특정 조건을 만족하는지 확인   

<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every>


## 자바스크립트는 어떻게 약속을 지킬까?

Promise, async/await, setTimeout이 브라우저에서 어떻게 동작하는지를 ECMAScript 표준 문서를 기반으로 추적하고 정리한 글이다.    
비동기 상태에 대한 처리는 항상 많이 이야기되었던 주제이기도 하지만 근본적으로 웹의 기능을 이해하기 위해 어떻게 접근해야 하는지를 알려주는 좋은 글   

<https://ui.toast.com/posts/ko_20220725>   


## 자바스크립트 async와 await   

<https://joshua1988.github.io/web-development/javascript/js-async-await/>   


## .fill()   

```TS
private getDayCategories(): string[] {
        const {selectedDateTime} = this.state

        return new Array(getLastDayOfMonth(selectedDateTime.getFullYear(), selectedDateTime.getMonth() + 1)).fill("")
            .map((value, index) => `${index + 1}일`)
    }
```

```TS 
// ES6 문법으로 이차원 배열 생성하는 방법
const arr = new Array(5).fill(0).map(() => new Array(4));
```


## 2차원 배열 new Array().fill()로 값 할당할 때 주의할 점   

<https://aeunhi99.tistory.com/257>   

## 피셔 예이츠 알고리즘

<https://velog.io/@choisy/Js-%ED%94%BC%EC%85%94-%EC%98%88%EC%9D%B4%EC%B8%A0-%EC%85%94%ED%94%8C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Fisher-Yates-Shuffle>   

# TS

## TypeScript에서 string key로 객체에 접근하기   
<https://soopdop.github.io/2020/12/01/index-signatures-in-typescript/>
