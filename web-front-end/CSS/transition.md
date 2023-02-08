# transition

- 시간을 두고 요소의 CSS를 전환 시킴

## transition-property

- 바꾸고자 하는 특정 속성을 선택 가능
- none, all, 속성 지정
- 기본 값 all

## transition-duration

- <time>
- 기본 값 0s

### time

- s : seconds
- ms : 1000ms = 1s

## transition-delay

- 전환될 때 지연 시간을 지정
- 기본 값 0s

## transition-timing-function

- 전환될 때 속도의 함수를 지정
- ease, ease-in, ease-out, ease-in-out, linear, cubic-bezier
- 기본 값 ease

## transition(shorthand)

- 기입되지 않은 값들은 기본 값으로 지정
- <time> 기입 시 순서대로 duration, delay로 지정
- 나머지는 순서 상관 없지만 property를 가장 먼저 쓰는 것을 권장

```css
div {
	transition: all 3s ease-in-out 1s;
}
```