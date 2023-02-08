# CSS개요

## CSS 소개

- CSS : Cascading Style Sheets
- 웹문서를 꾸며주는 파일
- css3부터 특징에 따라 모듈화됨
- font, table, animation 등 각 모듈 별로 버전이 다름(웹 브라우저별로 모듈의 지원 범위가 달라질 수 있음)
- cascading : 스타일요소의 상속을 의미
- CSS는 룰 기반의 언어
    - 룰 :

    ```css
    div {
    	color: red;
    	font-size: 12px;
    }
    ```

    - 선택자, 선언블럭(속성: 값)
- /*주석 내용*/
- html과 동일하게 코드 내에 개행을 무시함

### CSS 적용방법

- inline > embedded (> import) > external

```html
<head>
	<link rel="stylesheet" href="style/main.css" />
	<style>
		div {
			color: red;
		}
	</style>
</head>
<body>
	<div>
		<h2>hello</h2>
		<p style="color:green;"> world</p>
	</div>
<body>
```

- inline은 지양하고 selector를 이용하는 것을 권장

### 우선순위

- 사용자 구성(색약모드 등) > 개발자 선언 >  브라우저 정의
- 적용 범위가 적을 수록 우선시 (id > class > type(tag))
- 선언이 뒤에 올 수록 우선시