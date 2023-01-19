* CSS Transform 분할   
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
