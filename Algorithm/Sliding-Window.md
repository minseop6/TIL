# Sliding Window
- 배열이나 리스트의 요소들의 일정 범위 값을 비교할 때 사용하는 알고리즘
- 이름처럼 고정된 윈도우가 일정한 범위를 유지하면서 이동하는 알고리즘
- 시간복잡도: `O(n)`

```js
// 특정 크기의 부분 배열의 최대 값을 구하는 예제
function maxSumArr(arr, size) {
    let maxSum = 0;
    let tempSum = 0;
    if(arr.length < size) return null;
    for(let i = 0; i < size; i++) {
       tempSum += arr[i];
    }
    tempSum = maxSum;
    for(let i = size; i < arr.length; i++) {
       tempSum = tempSum - arr[i - size] + arr[i];
       maxSum = Math.max(tempSum, maxSum);
    }      
       return maxSum;
}
```