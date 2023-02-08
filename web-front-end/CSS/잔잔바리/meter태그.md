# meter 태그

- 설정된 범위 내에서의 게이지를 막대로 표시
- 제한적인 브라우저 지원(IE, 웹뷰 미지원)으로, 사용시 유의
- 계기를 표시할 때만 사용, 진행률은 progress태그를 사용할 것
- 속성 : low, high, max, min, optinum, value
- 스타일시트를 입히는 대신에 내용상에도 수치를 표기할 수 있고, js와 연동이 쉽다는 장점
- 막대 색 변화 : (블로그 퍼옴. 출처 하단에 표기)
    - 최솟값 <= 최적값 < 낮은 값: 숫자가 작을수록 이상적인 경우
        - 현재 값 <= 낮은 값: 초록색
        - 낮은 값 < 현재 값 <= 높은 값: 노란색
        - 높은 값 < 현재 값: 빨간색
    - 낮은 값 <= 최적값 <= 높은 값: 작지도 크지도 않은 중간 정도의 숫자가 이상적인 경우
        - 현재 값 < 낮은 값: 노란색
        - 낮은 값 <= 현재 값 <= 높은 값: 초록색
        - 높은 값 < 현재 값: 노란색
    - 높은 값 < 최적값 <= 최댓값: 숫자가 클수록 이상적인 경우
        - 현재 값 < 낮은 값: 빨간색
        - 낮은 값 <= 현재 값 < 높은 값: 노란색
        - 높은 값 <= 현재 값: 초록색

    즉 현재값이 최적값의 범위에 속하면 초록색, 최적값의 범위를 벗어나면 노란색, 최적값의 범위를 크게 벗어나면 빨간색으로 표시됩니다.

    참고로 low 속성을 생략할 경우 낮은 값은 최솟값과 같고, high 속성을 생략할 경우 높은 값은 최댓값과 같습니다. optimum 속성을 생략할 경우 최적값은 최솟값과 최댓값의 합을 2로 나눈 값(쉽게 말해서 최솟값과 최댓값의 정중앙)이 됩니다.

    ```html
    <ul>
      <li><meter value="2" min="0" max="10" low="3" high="7" optimum="0"> 2 / 10 </meter></li>
      <li><meter value="5" min="0" max="10" low="3" high="7" optimum="0"> 5 / 10 </meter></li>
      <li><meter value="8" min="0" max="10" low="3" high="7" optimum="0"> 8 / 10 </meter></li>
      <li><meter value="2" min="0" max="10" low="3" high="7" optimum="5"> 2 / 10 </meter></li>
      <li><meter value="5" min="0" max="10" low="3" high="7" optimum="5"> 5 / 10 </meter></li>
      <li><meter value="8" min="0" max="10" low="3" high="7" optimum="5"> 8 / 10 </meter></li>
      <li><meter value="2" min="0" max="10" low="3" high="7" optimum="10"> 2 / 10 </meter></li>
      <li><meter value="5" min="0" max="10" low="3" high="7" optimum="10"> 5 / 10 </meter></li>
      <li><meter value="8" min="0" max="10" low="3" high="7" optimum="10"> 8 / 10 </meter></li>
    </ul>
    ```

    출처 : 

    [http://parkjuwan.dothome.co.kr/wordpress/2021/07/04/html-meter-tag/](http://parkjuwan.dothome.co.kr/wordpress/2021/07/04/html-meter-tag/)