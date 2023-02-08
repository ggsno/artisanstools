# grid

## grid개요

- 이차원 레이아웃 시스템
- columns, rows로 구성
- 행과 열 사이에 공백을 gutters라고 부름

## container - display

- flexbox처럼 container와 item이 있음
- container-inside에 관한 속성이기 때문에 inline, block과 함께 사용 가능

## container - grid-template-rows, grid-template-columns

- <length>, fr
- repeat(반복횟수, 크기)

### grid-template-rows

- 값 갯수만큼 행을 만들고 값 크기만큼 행 크기 지정

### grid-template-columns

- 값 갯수만큼 열을 만들고 값 크기만큼 열 크기 지정

```css
.container {
  border: solid red 1px;
  display: inline-grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 50px);
  width: 150px;
}
```

## container - grid-template-areas

- 그리드 칸의 이름을 지정하여 문자열 형식으로 그리드 배치

```css
.container {
      border: solid red 1px;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-template-rows: repeat(4, 50px);
      width: 150px;
      grid-template-areas: 
        "hd hd hd hd"
        "mn mn . sd"
        "mn mn . sd"
        "ft ft ft sd"
    }
    .header {
      grid-area: hd;
    }
    .main {
      grid-area: mn;
    }
    .side {
      grid-area: sd;
    }
    .footer {
      grid-area: ft;
    }
    .item {
      font-size: 30px;
      border: solid 1px black;
      
    }
```

## container - row-gap, column-gap, gap(shorthand)

- 그리드 각 칸의 사이 공백 크기를 지정
- gap을 통해 한 번에 지정시 row, column 순으로 <length> 기입
- gap에 하나의 값만 주면 row,column 둘 다 적용
- 음수 불가

## container - grid-auto-rows, grid-auto-columns

- grid-template에서 명시적으로 부여된 행 열이 초과된 그리드의 행과 열의 크기를 지정
- grid-template은 명시적(없어도 자리 차지) grid-auto는 암시적(없으면 자리 차지하지 않음)

## container - grid-auto-flow

- 아이템들이 자리를 자동으로 찾아가는 기준점을 지정
- 값 : row(기본 값), column (, dense)
- 값에 dense를 추가 시 마크업 변경 없이 중간엔 빈 영역을 채워줌

## container - grid(shorthand)

- '/'를 기준으로 앞은 row, 뒤는 column에 대한 값들
- grid-template-row grid-template-column
- grid-auto-row,column은 auto-flow를 주면 기입 가능
- auto-flow를 '/'의 앞 뒤 위치에 따라 grid-auto-flow: row 혹은 column으로 지정 가능,

```css
.container {
      border: solid red 1px;
      display: grid;
      grid: 1fr 2fr / auto-flow 100px 200px;
      width: 300px;
    }
```

## container - justify-content, align-content

### justify-content

- 주축을 기준으로 그리드의 아이템을 정렬하는 방법을 지정
- 컨테이너에 남는 공간이 있어야 활용 가능
- 값  : start, end, space-between, space-around, center

### align-content

- 교차축을 기준으로 그리드의 아이템을 정렬하는 방법을 지정
- 컨테이너에 남는 공간이 있어야 활용 가능
- 값  : start, end, space-between, space-around, center

## container - justify-items, align-items

- 그리드 격자 안의 각각의 아이템에 대한 정렬
- stretch(기본 값). left, right, center

## Item - grid-row, grid-column (shorthand)

- grid-row-start, grid-row-end의 shorthand
- '/' 로 구분. start와 end를 순서대로 기입
- 값으로 정수가 올 수 있는데 이는 행의 넘버링이 아니라 격자선의 숫자(1부터 1씩 증가)
- 좌측과 상측부터 넘버링이 1씩 늘어나는데 반대편에 음수로 거꾸로 넘버링이 붙음
- 마이너스 넘버링은 명시적으로 선언된 그리드에만 붙음
- span을 통해 차지하는 행 열 수를 지정 가능

```css
.item {
	grid-row: 4 / span 2;
	grid-column: 2 / -1;
}
```

## item - grid-area (shorthand)

- grid-raw-start / grid-column-start / grid-raw-end / grid-column-end
- 문자열을 값으로 주면 container의 grid-template-area에의 이름으로 취급하고 '/'를 이용해 4개의 값을 주면 shorthand로 취급

## item - order

- 값 : <integer>
- 기본 0. 작은 값이 올 수록 앞으로 감

## item - z-index

- 값 : <integer>
- 기본 0. 작은 값이 올 수록 뒤로(아래로) 감

## grid 단위 - fr, min-content, max-content

- fr : <length>와 함께 사용 되면 length가 차지하고 남은 자리에서 비율만큼 자리를 차지
- min-content : 컨텐츠의 크기에 따라 요소 크기 변경하되 가장 작게.(영어 기준)내용 중 가장 큰 크기의 단어까지 크기가 줄어듦
- max-content :  컨텐츠 크기에 따라 요소 크기 변경하되 가장 크게

## grid 단위 - auto-fill, auto-fit

- auto-fill : 뷰포트가 늘어나서 컨테이너에 빈공간이 생겼을 때 열을 늘려서 채워줌
    - minmax : 늘어날 때 최소 최대 값을 지정
- auto-fit : 빈 공간이 생겼을 때 auto-fill과 같이 열을 늘려서 채워 주다가 열을 늘려도 아이템이 부족하면 아이템의 크기를 늘려 빈 공간을 차지
	
## grid 단위 - minmax()

- 최소 최대 값 설정
- minmax( [ <length> | <percentage> | min-content | max-content | auto ] , [ <length> | <percentage> | <flex> | min-content | max-content | auto ] )
```css
.container {
      display: grid;
      grid-template-columns: minmax(0,1fr) minmax(0,1fr) minmax(0,1fr);
    }
```
