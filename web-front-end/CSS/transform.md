# transform

## 개요

- <transform-function>
- **레이아웃의 변경 없이** 요소를 움직이거나 크기를 바꿈
- 함수 표기법을 이용
- 공백으로 함수를 구분해서 동시에 적용 가능
- 여러 개의 함수는 오른쪽부터 왼쪽으로 적용됨

## 크기 - scale()

- <number>(, <number>)
- 2차원 공간 조작만 가능
- scalex() 와 scaley()로 한 쪽 축만 조정 가능

## 회전 - rotate()

- <angle>

### <angle>

- 음수 가능
- 양수 = 시계 방향
- deg : degree
- grad : gradians
- rad : radians
- turn : 1turn = 360deg

## 이동 - translate()

- <length-percentage>
- x축, y축 순서대로 입력
- 한 가지만 입력시 x축만 이동
- 만약 rotate가 적용 되었을 시 회전한 상태 기준으로 이동
- <percentage>는 자기 자신의 width와 height 기준

## 기울이기 - skew()

- <angle>
- x축, y축 순서대로 입력
- 한 가지만 입력시 x축만
- skewX(), skewY()로 따로 입력 가능

## 기준점 - transform-origin

- <length-percentage>
- x축, y축 순서대로 입력
- 한 가지만 입력시 x축만
- 키워드 사용 가능 : center(기본 값), left, right, top, bottom

```css
img {
      width: 200px;
      transform: scale(0.8) rotate(0.3turn) translate(30px) skew(25deg);
      transform-origin: bottom right;
    }
```