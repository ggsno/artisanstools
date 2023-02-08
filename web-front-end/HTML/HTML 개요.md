# HTML과 웹 브라우저

## HTML과 웹 브라우저의 관계

- 웹 브라우저는 html 확장자의 뷰어이자 사용자에게는 웹 서핑을 도와주는 부가 기능을, 개발자에게는 웹 페이지를 분석할 수 있는 기능을 제공

## HTML : HyperText Markup Language

- hypertext : 웹 문서를 이루는 모든 요소. 문서를 통해 다른 문서로 이동할 수 있음
- markup language : 구조적 의미를 나타내는 언어

# HTML, CSS, Javascript

## 담당요소

- HTML : 구조. 웹문서의 골격
- CSS  : 표현. 각 요소들의 레이아웃, 스타일링
- JavaScript : 동작. 동적인 요소(사용자와의 인터렉션)
- 최근에는 js의 기능이 확장되면서 구분이 모호해졌으나 각각의 역할을 확실히 알고 있어야 독립적인 유지 보수 가능

## 왜 나눠야하는가?

- 재사용성. 같은 구조의 웹 페이지는 같은 html을 사용, css와 js도 동일

# 웹 표준, 웹 접근성, 웹 호환성

- 더 나은 웹 페이지를 만들기 위한 방향

## 웹 표준

- 각기 다른 웹 브라우저 간의 간극을 줄이기 위해 표준을 제시함
- HTML5 W3C에서 2014년에 공식 표준화.
- 2019년에 WHATWG에서 HTML Living Standard가 표준화 되었지만 이를 편의상 여전히 HTML5로 부름

## 웹 접근성

- 환경으로 인한 제약 혹은 장애에 대한 대비.

## 웹 호환성

- 웹 브라우저 버전, 종류에 영향 받지 않도록 대비.
- 웹 표준 준수를 통해 이룰 수 있음

# HTML 기본

## Tag

- 웹페이지를 구성하는 요소(element)를 감싸는 표기법.
- opening tag, contents, closing tag로 이루어짐
- HTML5 웹 표준에 맞게 작성
- **대소문자를 구분하지 않지만 웹 표준에서는 모두 소문자로 작성하는 것을 권장**

## 빈 요소(Empty element)

- 내용이 없는 요소 (이미지, 수평선, 줄바꿈 ... )
- 닫는 태그 없어도 됨
- **웹 표준에 해당 요소가 명시되어있음. 빈 요소로 명시되어있지 않은 태그(div, p ...)를 내용 없이 쓰더라도 빈 요소가 아님.**
- 태그 뒤에 '/'를 쓰는 경우도 있음. (예시 : <br/>) 이는 optional 하지만 동일 프로젝트에선 한가지 방법으로 통일하는 것을 권장.

## 요소의 중첩(Nesting)

- 요소 안에 다른 요소를 포함 가능.
- 구분을 위해 들여쓰기를 사용

## 주석(Comments)

- <!-- 주석입니다-->

## HTML문서의 구조

```html
<!DOCTYPE html>
<html>
	<head>
		<!-- 해드 태그-->
	</head>
	<body>
		<!-- 바디 태그-->
	</body>
</html>
```

- <!DOCTYPE html> : <html5 표준 이전에는 html 버전을 명시해야 했지만 지금은 관습적으로 사용.
- <html> : 페이지 전체의 내용을 감싸는 root 요소
- <head> : 화면에 직접적으로 보이지 않는 웹페이지 정보
    - meta tag : 문서의 일반적인 정보와 인코딩 명시
- <body> : 화면에 나타나는 모든 내용

### head 태그

- 기계(브라우저)가 식별할 수 있는 문서 정보(메타데이터)를 가짐.
- 사람이 읽을 수 있는 정보는 header 태그를 사용
- html5 호환 브라우저는 head태그가 없을 경우 자동으로 생성하지만 명시적으로 적는 것을 권장.

[HEAD - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/HEAD)

### body 태그

- 사용자에게 보여지는 html문서의 내용을 나타냄
- 한 문서에 하나만 존재할 수 있음

[: The Document Body element - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/body)

- [참고] MDN에서 나오는 속성 중 옆에 쓰레기통 아이콘은 웹 표준에 맞지 않는 것.

## 태그를 구분 짓는 특성

### 구획을 나누는 태그

- 단독으로 사용했을 때 눈에 보이지 않음
- 여러 요소를 묶어서 그룹화 시켜줌

### 그 자체로 요소인 태그

- 단독으로 사용해도 눈이 보임.

### 블록(block)

- 언제나 새로운 줄에서 시작함
- 가로 길이를 명시하지 않으면 좌우 양쪽으로 최대한 늘어나 가능한 모든 너비를 차지. 이 때 최대 길이는 부모 요소가 허용한 최대치 까지.

### 인라인(inline)

- 줄의 어디든 시작될 수 있음.
- 바로 이전 요소가 끝나는 지점부터 시작, 요소의 내용만큼 자리 차지
- **인라인 요소 안에 블록 요소를 포함할 수 없음**
- **내가 사용하는 태그가 블록 요소에 속하는지  인라인 요소에 속하는지 정확히 알아야 함**

### 콘텐츠 카테고리

- 웹 표준에서 나눈 요소의 카테고리

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/179020fa-0dbd-4d97-bf85-9cb71a40adb0/Untitled.png)

- metadata : 문서의 메타정보. 해드 태그
- flow : 일부 메타데이터를 제외한 모든 요소
- section : 구획을 나누는 요소
- heading : 제목과 관련된 요소
- phrasing : 문단에서 텍스트를 마크업할 때 사용
- embedded : 이미지, 비디오 등 외부 소스를 가져오거나 삽입할 때 사용
- interactive : 사용자와의 상호작용을 위한 요소

# 메타데이터 요소

- 메타데이터 : 데이터를 설명하는 데이터
- 검색엔진은 메타데이터를 통해 데이터를 분류함

## title

- 문서 제목. 브라우저의 제목 표시줄에 표기됨
- 태그 안 쪽에 태그가 중첩되면 무시
- 유일함
- 타이틀에 의해 검색엔진이 상위에 띄워줄 확률이 높으므로 잘 지어야 함
- 타이틀을 명사의 나열로 정하면 광고로 인식할 수 있으므로 페이지에 대한 간략한 설명을 기입하는 것을 권장

## meta

- 다른 메타 관련 요소로 나타낼 수 없는 메타데이터를 나타냄
- 빈 요소임 (속성 값으로 구분)
- 여러 개의 메타 데이터 존재 시 새로운 메타 태그 생성해서 사용

```html
<meta name="application-name" content="movie-app"/>
<meta name="auythor" content="ks"/>
```

### meta - 문자 인코딩

- 다양한 나라의 언어를 지원하기 위해 인코딩 정보를 기입
- head태그의 맨 윗부분이나 tilte 앞부분에 위치하는 것을 권장

```html
<meta charset="UTF-8" />
```

### meta - 뷰포트

- 다양한 화면에 따라 달라지는 view를 설정하기 위함
- 쉼표로 구분

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

[표준 메타데이터 이름 - HTML: Hypertext Markup Language | MDN](https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta/name#html_%EB%AA%85%EC%84%B8%EA%B0%80_%EC%A0%95%EC%9D%98%ED%95%98%EB%8A%94_%ED%91%9C%EC%A4%80_%EB%A9%94%ED%83%80%EB%8D%B0%EC%9D%B4%ED%84%B0_%EC%9D%B4%EB%A6%84)

## MIME 타입

- 외부파일을 끌어다 쓸 때, 문자열로 이루어진 경로를 해석(확장자를 알아내기)하기 위해 타입을 적어줌
- type="type/subtype"
- 대소문자 구분하지 않지만 소문자 권장

```html
<link href="style/main.css" rel="stylecheet" type="text/css" />
```

[MIME 타입 - HTTP | MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

## style

- html 내부에 css 스타일을 적용할 수 있는 태그
- 외부 파일로 분리하는 것을 권장

## script

- script파일을 직접 쓰거나 불러올 수 있는 태그
- 스크립트 태그는 body태그 뒤에 오는 것이 랜더링에 유리하므로 body 태그 맨 아래에 위치 하는 것을 권장
