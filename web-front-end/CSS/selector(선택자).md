# 선택자(selector)

## 속성 선택자

- type[attr]
- type[attr=value] : input태그에서 type에 따라 달리 선택할 때 많이 사용
- type[attr^=value] : value로 시작하는 것 선택
- type[attr$=value] : value로 끝나는 것 선택
- type[attr*=value] : value를 포함하는 것 선택
- class, id 또한 동일하게 사용 가능

```css
/* type[attr] */
a[target] {
  color: hotpink;
}

/* type[attr=value] */
input[type="submit"] {
  background-color: green;
}

/* type[attr^=value] */
a[href^="http://"] {
  color: red;
}

/* type[attr$=value] */
a[href$=".com"] {
  color :lawngreen;
}

/* type[attr*=value] */
a[href*="example"] {
  color: slateblue;
}
```

## 가상클래스 선택자(pseudo-class selector) ':'

### first-child, last-child, nth-child

- first-child : 해당 선택자의 **부모 요소의 첫 번째 요소**를 선택. 선택자의 부모 요소의 첫 번째 요소가 해당 선택자를 가지고 있지 않으면 무시됨
- last-child : 해당 선택자의 **부모 요소의 마지막 요소**를 선택
- nth-child : 해당 선택자의 부모 요소의 n번째 요소 선택. 자연수 뿐만 아니라 even, odd, 2n-1 등 올 수 있음

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    .movie:first-child {
      color: aquamarine;
    }
  </style>
</head>
<body>
  <ul>
    <li>list</li> <!-- no colored-->
    <li class="movie">list</li>
    <li class="movie">list</li>
    <li class="movie">list</li>
  </ul>
<body>
</html>
```

### first-of-type, last-of-type, nth-of-type

- first-of-type : 해당 선택자의 동일 타입 요소들의 첫 번째 요소를 선택
- last-of-type : 해당 선택자의 동일 타입 요소들의 마지막 요소를 선택
- nth-of-type : 해당 선택자의 동일 타입 요소들의 n번째 요소를 선택

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    .movie:first-of-type {
      color: aquamarine;
    }
  </style>
</head>
<body>
  <div class="movie">mo1</div> <!--colored-->
  <p class="movie">mo2</p> <!--colored-->
  <p class="movie">mo3</p>
  <div class="movie">mo4</div>
  <div class="movie">mo5</div>
<body>
</html>
```

### not

- selecto:not(selector)

## 동적가상 클래스 선택자

- 유저의 동작에 따라 동적으로 바뀌는 스타일링을 위해 사용

### link, visited

- 하이퍼링크의 상태(방문 기록)에 따라 선택
- link : 미방문
- visited : 방문

### hover, active, focus

- hover : 마우스를 올렸을 때 선택
- active : 마우스를 누르고 있는 동안 선택.
    - LVHA 순서로 쓰는것을 권장 (link visitied hover active
- focus : 특정 요소에 포커싱(탭으로 선택, 텍스트 입력 등) 된 것을 선택

### enabled, disabled, checked

- input타입에 많이 사용됨
- disabled : disabled 속성이 true가 된 요소를 선택
- checked : checked 속성이 true가 된 요소를 선택

## 가상요소 선택자 pseudo-element selector '::'

- 콜론을 하나만 사용해도 동작함
    - css3 부터 가상클래스와 가상요소를 구분하기 위해 표기가 나뉘었음
- content 속성을 통해 문자열로 요소를 넘겨줌
- content 속성을 통해 넘어온 요소는 스타일요소로 간주하여 화면에서 드래그로 선택이 안됨

### before, after

- 요소의 이전, 이후에 가상요소 삽입

### first-letter, first-line, selection

- first-letter : 첫 번째 문자를 선택. before로 생성된 요소 또한 고려함
- first-line : 첫 번째 줄을 선택. 화면 크기에 따라 달라지는 줄 고려함
- selection : 선택(드래그)된 영역 선택

## 선택자 결합 - 하위, 자식

- 하위 : ' '(공백)으로 구분
- 자식 : '>'으로 구분

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    .temp li:first-of-type {
      color: red;
    }

    .temp > li:last-of-type {
      color: blue;
    }
  </style>
</head>
<body>
  <ul class="temp">
    <li>list</li> <!-- red colored-->
    <ul>
      <li>list</li> <!-- red colored-->
      <li>list</li>
    </ul>
    <li>list</li>
    <li>list</li> <!-- blue colored-->
  </ul>
<body>
</html>
```

## 형제 선택자, 그룹화

### 일반 형제 선택자 결합 ('~')

- '~' 앞의 선택자를 기준으로 형제 요소 중 뒤에 오는 요소를 선택

### 인접 형제 선택자 결합 ('+')

- '+' 앞의 선택자를 기준으로 형제 요소 중 바로 뒤에 오는 요소를 선택

### 그룹화 (',')

- 여러 개의 요소를 동시에 선택

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    p ~ div {
      color: red;
    }
    code + p {
      color: blue;
    }
  </style>
</head>
<body>
  <div>
    <p>p</p>
    <div>div <!--red colored-->
      <p>p</p> <!--red colored-->
    </div>
    <p>p</p>
    <code>code</code>
    <p>p</p> <!--blue colored-->
    <p>p</p>
  </div>
<body>
</html>
```

## 범용 선택자

- '*' 으로 모든 요소를 선택함

## 상속 제어하기

### initial

- 속성 값으로 initial을 주면 해당 속성을 상속 받지 않음
- all 속성에 initial을 주면 모든 속성을 상속 받지 않음

### inherit

- 속성 값으로 inherit을 주면 해당 속성을 상속 받게 됨

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
   .child1 {
     color: red;
   }
   .parent1, .parent2 {
     color: blue;
   }
   .parent2 * {
     color: inherit;
   }
  </style>
</head>
<body>
  <div class="parent1">
    parent1 <!--blue-->
    <div class="child1">child1</div> <!--blue-->
    <div class="child2">child2</div> <!--red-->
  </div>
  <div class="parent2">
    parent2 <!--blue-->
    <div class="child1">child1</div> <!--blue-->
    <div class="child2">child2</div> <!--blue-->
  </div>
<body>
</html>
```

### unset

- 상속 받을 값이 있을 때 inherit, 없을 때 initial
- 자신에게 직접 부여된 값이나 기본 값을 무시하고 상속 받은 값만 유지

## 우선순위

1. !important
2. 선언된 곳(inline > embedded > external)
3. 명시도 (적용 범위가 좁을수록 명시도가 높음)
4. 코드 위치