# async, defer

## js 불러오기

- 웹에서 외부 스크립트를 불러올 때 script 태그를 삽입함
- 이 때 script 태그의 위치에 따라 스크립트의 처리 순서가 결정됨
- 브라우저의 html parser가 스크립트 태그에 도달하면 해당 스크립트를 처리하고 나머지 부분을 파싱함
- 때문에 head태그에 script태그를 선언했다면 body에 도달하기 전에 스크립트를 처리하므로 본문이 늦게 뿌려질 수 있음
- body의 맨 끝부분에 script를 선언함으로써 이를 해결할 수 있음

## async, defer 배경

- body 맨 끝부분에 script를 선언한다 하더라도  html문서 자체가 매우 크면 페이지가 매우 느려질 수 있음
- html5에서 이를 해결하기 위해 script 속성으로 async와 defer를 추가함
- 둘 다 boolean형
- html파싱과 스크립트 다운로딩(fetch)을 병렬로 진행함
- **head태그에 삽입된 script에만 의미가 있음** body태그에 삽입한 script에는 의미 없음

### async

- 스크립트가 사용가능할 때 즉시 실행함
- defer와 동시에 선언 시 defer만 지원되는 구식 브라우저가 아니라면 async가 우선시 됨
- 문서 내 순서와 상관 없이 먼저 다운로드 된 스크립트가 먼저 실행됨

### defer

- 전체 문서가 파싱된 후에 스크립트가 실행됨
- 문서에 추가된 순으로 스크립트가 실행됨

## 웹 페이지 로딩 시나리오

### defer 또는 async 없이 <head>에 script 삽입

- html 파싱 시작 → head에서 스크립트를 fetch 후 실행 → 나머지 html 파싱
- 파싱이 스크립트를 가져와서 실행이 완료될때 까지 중단되었다가 완료 후에 파싱이 다시 진행
- DOM생성 전에 DOM을 조작하는 스크립트가 실행되어 오류 발생 가능

### defer 또는 async 없이 <body>맨 마지막에 script 삽입

- html 파싱 시작, body요소를 모두 랜더링 후 → 스크립트 fetch, 실행
- 이전 케이스보다 사용자에게 빈 화면 띄우는 시간이 줄어듦

### async를 사용하여 <head>에 script 삽입

- html 파싱 시작, head에서 멈추지 않고 비동기로 스크립트를 fetch → fetch가 완료되면 html파싱을 멈추고 스크립트를 실행 → 실행 완료 후 html파싱 재개
- 경우에 따라 DOM생성 전에 DOM을 조작하는 스크립트가 실행되어 오류 발생

### defer를 사용하여 <head>에 script 삽입

- async와 마찬가지로 비동기로 스크립트를 fetch하지만 fetch 완료 후 바로 실행되지 않고 html파싱이 완료된 후에 실행됨

## 언제 사용하나

- defer는 DOM 전체가 필요한 스크립트나 실행 순서가 중요한 경우에 사용
- async는 방문자 수 카운트나 광고 등과 같이 독립적이거나 실행 순서가 중요하지 않을 때 사용

참고 :

[https://ko.javascript.info/script-async-defer](https://ko.javascript.info/script-async-defer)

[https://rottk.tistory.com/entry/외부-JavaScript-불러오기-async-defer](https://rottk.tistory.com/entry/%EC%99%B8%EB%B6%80-JavaScript-%EB%B6%88%EB%9F%AC%EC%98%A4%EA%B8%B0-async-defer)