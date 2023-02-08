# css variable

### 선언

- --[변수 명]: [값]

```css
:root {
	--var1-color: red;
	--var2-url: url("img/image1.jpg");
	--var3 : ;
}
```

- 대소문자 구분
- 하위 요소에 상속됨

### 사용

- [요소]: var(--[변수 명](, [default 값]);

```css
div {
	color: blue; /* <1> */
	color: var(var1-color, orange); /* <2> */
}
```

- var를 지원하지 않는 브라우저 → <1>적용 (blue)
- var1-color에 값이 없을 때 →<2>의 default값 적용 (orange)
- var1-color 값 있을 때 → <2>의 var1-color값 적용
- default값으로 변수 삽입 가능

## 적용 시 유의사항

- 변수 값으로 숫자 사용 시 공백 발생으로 값과 단위가 각각의 토큰으로 인식됨
- 단위도 함께 선언하거나 calc함수를 통해 값을 넣어야 함

```css
.bad {
	--var1-size: 50;
	width: var(var1-size)vw; /* 50 vw로 변환되어 값이 무시됨*/
	height: var(var1-size)vh; /* 50 vh로 변환되어 값이 무시됨*/
}
```

```css
.good {
	--var1-size: 50;
	width: calc(var(var1-size) * 1vw); 
	height: calc(var(var1-size) * 1vh);
}
```

- url을 변수에 넣을 시, 구문 전체를 넣어야 정상적으로 작동 되고 문자열을 따로 전달 불가능

```css
/* CSS LIMITATION */ 
--img: "sample.jpg"; background: url("img/" var(--img)); 
/* CSS BUG */ 
--img: "img/sample.jpg"; background: url(var(--img)); 
/* ★★★ GOOD ★★★ */ 
--img: url("img/sample.jpg"); background: var(--img);
```

- 변수를 변수로 재선언 시 값이 사라짐

```css
:root {
	--accent: green;
	--accent: var(--accent); 
} 
body {
	background: red; 
} 
h1 {
	background: blue;
	background: var(--accent, orange); /* 값이 사라져서 orange로 됨*/
}
```

- 브라우저가 변수를 지원하는지 간단히 확인하기 위해 @supports 어노테이션 사용할 수 있음

```css
body {
  background: red;
}
@supports (--css: varibales) {
  body {
    background: yellow;
  }
}
```
참고 : [https://fresh-mint.tistory.com/entry/css-variable-변수-총-정리](https://fresh-mint.tistory.com/entry/css-variable-%EB%B3%80%EC%88%98-%EC%B4%9D-%EC%A0%95%EB%A6%AC)