## OpenGraph

- 링크를 미리 볼 수 있는 메타 데이터 정보 프로토콜
- 웹 페이지가 소셜미디어, 혹은 오픈그래프를 활용한 사이트에 공유될 때 사용됨 (ex 페이스북 링크, 카카오톡 링크 공유 등에서 링크대상을 미리 볼 수 있는 제목이나 설명 글 따위)
- og:image : 미리 보여줄 이미지
- og:title : 링크의 타이틀, 지정되어있는 title 태그보다 우선시 됨
- og:description : 링크의 설명, 지정되어있는 description 요소의 내용보다 우선시 됨

```html
<head>
	<meta property="og:title" content="IU collection">
	<meta property="og:description" content="210518 IU best photos">
	<meta property="og:image" content="./img/IU-main.png">
</head>
```

- 이외에 다양한 속성이 있음

[http://ogp.me/](http://ogp.me/)

## robots.txt과 meta robots 태그 차이점

### 크롤링 제어와 인덱싱 제어

#### 크롤링

- 검색 엔진이 하이퍼링크를 타고 돌아다니면서 문서를 수집하는 것
- robots.txt에서 제어

#### 인덱싱

- 크롤링을 한 문서들을 사용자에게 제공하기 용이하게 인덱싱하는 것
- meta robots 태그에서 제어