# 이진 탐색 시 pivot 지정 고려 사항

### 예시문제

[Search Insert Position - LeetCode](https://leetcode.com/problems/search-insert-position/submissions/888551076/?envType=study-plan\&id=algorithm-i)

> Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
>
> You must write an algorithm with `O(log n)` runtime complexity.

### 완벽하지 않은 풀이

```jsx
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    const findIndex = (startIndex, endIndex) => {
        const pivotIndex = Math.floor((startIndex + endIndex) / 2);
        const pivotValue = nums[pivotIndex];
        
        if (pivotValue === target)
            return pivotIndex;
        if (startIndex === endIndex)
            return target < pivotValue ? pivotIndex : pivotIndex + 1;
        if (target < pivotValue)
            return findIndex(startIndex, pivotIndex - 1);
        if (pivotValue < target)
            return findIndex(pivotIndex + 1, endIndex);
        throw new Error("unexpected");
    }

    return findIndex(0, nums.length - 1)
};
```

### 위의 코드에서 문제점 찾기

오답케이스 ::

nums = \[1,2]

target = 0

해설 ::

target < pivotValue일 때 재귀함수의 매개변수 endIndex에 pivotIndex - 1을 전달함

* 찾고자 하는 target 값보다 기준(pivot) 값이 크므로 기준 값을 제외한 범위를 탐색하고자 함
* 기준 값을 제외한 나머지 범위가 없는 경우가 발생 :
  * \[1, 2]에서 0을 찾기
    1. pivotIndex = Math.floor((0 + 1) / 2) // 0
    2. target < pivotValue // 0 < 1
    3. findIndex(0, -1) // 유효하지 않은 범위
* 해결방법 ::
  * 첫 번째 방법 : 유효하지 않은 범위 예외 처리 (지저분함)
  * 두 번째 방법: 탐색 범위 조정 시 pivot을 제외하지 않기
    * 문제 상황은 endIndex가 -1이 된 경우만 존재하므로 target이 기준값보다 큰 상황은 제외해도 무관
