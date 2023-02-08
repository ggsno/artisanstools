# animation

- transition보다 다수의 스타일을 전환 할 수 있음

## @keyframes

- <percentage> 혹은 키워드 from과 to 사용 가능
- 애니메이션에서 사용할 키 프레임을 함수같이 미리 만들어 놓음
- 첫 값(from, 0%)이나 끝 값(to, 100%)을 지정하지 않으면 원 상태로 취급

```css
@keyframes animationName {
	from { width: 100px }
	to { width: 300px }
}

@keyframes temp {
	0% { background-color: black }
	50% { background-color: red }
	100% { background-color: white }
}

@keyframes temp2 {
	75% { transform:translate(30px) } 
/*Since the end value is not specified, 
move 30 pixels and return to its original position.*/
}
```

## animation-name

- 상속 안됨
- 예악어를 사용하지 않도록 주의 (initial, inherit, revert, unset)

## animation-duration

- <time> 음수 무시
- 키프레임 하나가 끝나는 주기
- 

## animation-dalay

- <time> 음수 가능
- 지연시간
- 음수 지정 시 애니메이션이 즉시 실행되지만 해당 음수 값만큼 미리 시작된 것처럼 주기가 설정됨

## animation-timing-function

- transition-timing-function과 동일
- 전환될 때 속도의 함수를 지정
- ease, ease-in, ease-out, ease-in-out, linear, cubic-bezier
- 기본 값 ease

## animation-iteration-count

- 반복 횟수
- <number> 혹은 infinite
- 실수(real number)로 지정 가능(0.5 입력 시 50%만 실행하고 종료)

## animation-direction

- 재생 방향
- normal(기본 값), reverse, alternate, alternate-reverse

## animation-play-state

- 애니메이션 일시 정지, 재생
- running(기본 값), paused

## animation-fill-mode

- 애니메이션이 시작하기 전, 후에 키프레임에 있는 값을 사용할지 말지
- none(기본 값), forwards, backwards, both
- forwards : 애니메이션 끝나고 마지막(100%, to) 키프레임 값 사용
- backwards : 애니메이션 시작 전에 첫(0%, from) 키프레임 값 사용
- both : 둘 다 사용

## animation(shorthand)

- <time>은 duration, delay 순으로 해석
- name과 duration은 필수