# flexbox

- css3 이후에 나온 개념
- div를 가로 정렬하고 싶어!
    - inline-block으로 바꾸면 사이에 margin이 아닌 공백이 생김
    - float를 주면 clear나 다른 처리가 필요함
- 가로 혹은 세로 정렬을 하기 위해 나온 개념
- container와 item이 함께 나와야 의미가 있음(정렬이니까)
- 1차원. 한 줄에 대한 속성 (2차원은 grid)

## 용어

### flex container, flex item

- 부모 자식 관계를 확실히 알아야 함
- container에 사용할 수 있는 속성과 item에 사용할 수 있는 속성이 나뉘기 때문

### main axis, cross axis

- 주축(가로, 왼→오)과 교차축(세로, 위→아래)
- 축은 바뀔 수 있음

## container - display

- display-outside : 요소 바깥쪽의 관계 - block, inline
- display-inside : 요소 안쪽의 관계 - flex

## container - flex-direction

- 컨테이너 내의 아이템을 배치할 때 사용할 주축 및 방향을 지정
- row : 좌 → 우(기본 값)
- row-reverse : 우 → 좌
- column : 상 → 하
- column-reverse : 하 → 상

## container - flex-wrap

- 하위에 있는 아이템 요소들이 강제로 한 줄에 배치되게 할지, 개행되게 할지 지정
- nowrap : 아이템이 컨테이너보다 더 크면 해당 값을 줄여서 한 줄에 오게 함(기본 값)
- wrap : 여러 행으로 개행됨 (짜부가 안 되고 아이템의 모양을 잃지 않음)
- wrap-reverse : 개행이 반대 방향으로 됨

## container - flex-flow(shorthand)

- flex-direction과 flex-wrap을 한 번에 쓸 수 있는 속성

```css
div {
	flex-flow: column wrap
}
```

## item - order

- 플랙스 또는 그리드 컨테이너 안에서 현재 요소의 배치 순서를 지정
- 기본은 0
- 오름차순 (order가 크면 뒤로, 작으면 앞으로)
- 값 : <integer>
- 화면에 보이는 순서에만 영향을 줌(탭 순서에 상관 없음)
- 부모가 flex여야 적용 가능

## item - flex-grow, flex-shrink, flex-basis

### flex-grow

- 자신이 가진 공간보다 더 넓게 차지할 수 있게 함
- 할당 가능한 공간이 남았을 때 모두 사용하게끔 함
- 값 : <number> 음수 불가. 기본 0
- 모든 아이템 동일한 grow를 가지고 있으면 동일하게 공간을 할당(컨텐츠 크기가 아닌 추가로 늘어나는 공간을 할당하는 것)
- 값의 크기에 따라 남은 공간의 비율을 나눠서 할당(기본 0)

### flex-shrink

- grow와 반대로 공간보다 아이템이 클 때 줄어드는 속성
- 값 : <number> 음수 불가. 기본 1

### flex-basis

- 플랙스 아이템의 초기 크기를 지정(grow나 shrink되지 않은 상태)
- 값 : <'width'> (<length> <percentage>)
- 기본 auto
- 값을 지정하지 않으면 내용의 크기에 따라 너비가 달라지는데 grow와 shrink값은 추가로 할당한 부분만을 계산하므로 최종 너비를 지정하는 데에 어려움이 있을 수 있음
- 속성 값을 0으로 설정하면 flex item이 absolute flex item이 되어 **flex container를 기준**으로 크기가 결정됨
- 속성 값을 auto로 설정하면 flex item이 relative flex item이 되어 **컨텐츠의 크기를 기준**으로 크기가 결정됨

## item - flex(shorthand)

- grow, shrink, basis를 한 번에 지정
- **1~2개 값을 지정했을 때 basis값은 기본 값인 auto가 아니라 0이 됨**
- 값 갯수 :
    - 1개 : <number>면 grow, <length>또는<percentage>면 basis
    - 2개 : 첫 번째 값은 <number>여야 하고 grow가 됨. 두 번째 값은 shrink나 basis
    - 3개 : grow, shrink, basis 순서대로 사용
- 키워드 값 :
    - initial : 0 1 auto (찌그러들 수 있지만 늘어나진 않음)
    - auto  : 1 1 auto (찌그러들 수도 있고 늘어남)
    - none : 0 0 auto (변함 없음)
```css
.item {
  flex: 1; /* flex: 1 1 0 과 동일*/
}
```

## container - justify-content

- 주축을 기준으로 아이템들을 어떻게 정렬할 것인지 지정
- flex-start : 주축이 시작하는 위치에 정렬
- flex-end : 주축이 끝나는 위치에 정렬
- center : 주축의 가운데 위치에 정렬
- space-between : 주축의 양 끝(여백 없음)에 정렬하고 사이 간격을 동일하게 정렬
- space-around : 주축의 양 끝(앞 뒤 동일하게 여백을 줌)에 정렬하고 사이 간격을 동일하게 정렬

## container - align-items

- 교차축을 기준(한 줄)으로 아이템을 어떻게 정렬할 것인지 지정
- 한 줄 안에서의 세로에 대한 속성
- stretch : 교차축 전부 차지 (기본 값)
- flex-start : 교차축의 시작에 정렬
- flex-end : 교차축의 끝에 정렬
- center : 교차축의 가운데에 정렬
- space-between이나 space-around는 한 줄에 대한 속성이기 때문에 없음
- wrap으로 개행 된 것들의 정렬은 align-content를 이용

## container - align-content

- 교차축을 기준(여러 줄)으로 아이템을 어떻게 정렬할 것인지 지정
- flex-start : 교차축의 시작에 정렬
- flex-end : 교차축의 끝에 정렬
- center : 교차축의 가운데에 정렬
- space-between : 교차축의 양 끝(여백 없음)에 정렬하고 사이 간격을 동일하게 정렬
- space-around :교차주축의 양 끝(앞 뒤 동일하게 여백을 줌)에 정렬하고 사이 간격을 동일하게 정렬

## item - align-self

- align값을 한 요소(아이템)에 따로 적용