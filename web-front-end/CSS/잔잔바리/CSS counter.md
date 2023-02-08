# CSS counters

- 요소가 몇 번 사용되었는지 추적하여 따라 번호를 매길 수 있음
- counter-reset : 초기화할 변수를 지정. 카운터속성을 사용하기 위해 반드시 필요
- counter-increment : 해당 변수의 카운터를 1씩 증가시킴

## counter

- counter함수 : counter([name]) 혹은 counter([name], [style])

```css
body {
  counter-reset: section;                       /* counter 이름을 'section'으로 지정합니다.
                                                   초깃값은 0입니다. */
}

h3::before {
  counter-increment: section;                   /* section의 카운터 값을 1씩 증가시킵니다. */
  content: "Section " counter(section) ": ";    /* section의 카운터 값을 표시합니다. */
}
```

### 응용 - 내용 없는 링크에만 counter 넣기

```css
:root {
  counter-reset: link;
}

a[href] {
  counter-increment: link;
}

a[href]:empty::after {
  content: "[" counter(link) "]";
}
```

```html
<p>See <a href="https://www.mozilla.org/"></a></p>
<p>Do not forget to <a href="contact-me.html">leave a message</a>!</p>
<p>See also <a href="https://developer.mozilla.org/"></a></p>
```

## 중첩 카운터

- counters함수 : counter([name], [string]) 혹은 counter([name], [string], [style])

```css
ol {
  counter-reset: section;                /* ol 요소마다
                                            이름이 section인
                                            새 인스턴스를 생성합니다. */
  list-style-type: none;
}

li::before {
  counter-increment: section;            /* 해당 인스턴스 안에서
                                            section 카운터 값 증가 */
  content: counters(section, ".") " ";   /* section 카운터 값을
                                            마침표(.)로 구분해 결합하여
                                            표시합니다. */
}
```

```html
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item               <!-- 2     -->
    <ol>
      <li>item</li>      <!-- 2.1   -->
      <li>item</li>      <!-- 2.2   -->
      <li>item           <!-- 2.3   -->
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
        </ol>
        <ol>
          <li>item</li>  <!-- 2.4.1 -->
          <li>item</li>  <!-- 2.4.2 -->
          <li>item</li>  <!-- 2.4.3 -->
        </ol>
      </li>
      <li>item</li>      <!-- 2.4   -->
    </ol>
  </li>
  <li>item</li>          <!-- 3     -->
  <li>item</li>          <!-- 4     -->
</ol>
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item</li>          <!-- 2     -->
</ol>
```

코드 출처 : [https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters)