# [AL] 최장 증가 수열(LIS)

# 1. 최장 증가 수열(LIS, Longest Increasing Sequence)

- 원소가 N개인 배열의 일부 원소를 골라내어 만든 부분 수열 중 각 원소가 이전 원소보다 크다는 조건을 만족하고 그 길이가 최대인 부분 수열
- 순서는 유지되어야 한다.
- 예시
    - [7, 2, 3, 8, 4, 5] 중 가장 긴 증가하는 부분 수열은 [2, 3, 4, 5]

## 1-1. 구현 방법(DP)

```
// DP를 이용한 LIS
int lis_dp(int n){
    int max = 1;
    for(int i=0;i<n;i++){
        dp[i] = 1;
        for(int j=0;j<i;j++){
            if(arr[j] < arr[i] && dp[j]+1 > dp[i]){
                dp[i] = dp[j]+1;
                if(max < dp[i]){
                    max = dp[i];
                }
            }
        }
    }
    return max;
}
```

1. i는 0부터 배열 전체를 순회하고  j는 0부터 i 이전까지 순회
2. arr[j] < arr[i]
    - i 이전 값들이 현재의 i 값보다 작은 지 확인 → 증가하는 수열의 형태인지 확인
3. dp[j]+1 > dp[i]
    - j번째 원소를 마지막으로 갖는 최대 증가 수열(dp[j])  끝에 arr[i]값을 추가했을 때 현재까지의 최대값보다 커야함
4. max값을 갱신해주며 LIS의 길이를 반환

- 시간복잡도
    - O( N^2 )
    

## 1-2. 구현 방법(이진 탐색)

### 1-2-1. 이진 탐색 라이브러리

```jsx
int[] values = {3, 11, 15, 20, 21, 45};
		
		System.out.println(Arrays.binarySearch(values, 3)); // 0
		System.out.println(Arrays.binarySearch(values, 45)); // 5
		System.out.println(Arrays.binarySearch(values, 11)); // 1
		System.out.println(Arrays.binarySearch(values, 30));	// -6 : 찾다가 멈춘 위치, 예상대로라면 있을 위치
		
		// -1 :  -0은 없으므로 +0을 주면 0번째 자리에 있는 값이라 착각할 수 있으므로 -(들어갈 갔어야할 위치)-1로 리턴한다.
		// 값을 못찾으면 들어있었어야할 위치 값을 알 수 있다.
		System.out.println(Arrays.binarySearch(values, 1));	// -1
		System.out.println(Arrays.binarySearch(values, 50));	// -7 : 6이라는 인덱스에 위치해어야할 위치
		
		// binarySearch(arr, from, to, target) : from : 포함, to : 미포함
		// 배열 내에 같은 숫자가 2개 이상 존재한다면 먼저 탐색한 값을 줄 것
		System.out.println(Arrays.binarySearch(values, 1, 4, 45)); // -5
```

### 1-2-2. LIS 구현

```jsx
int size = 0;	// LIS에 채워지는 원소수
		for(int i = 0; i < N; i++) {
			// 존재하지 않는 값을 찾으므로 들어갈 위치를 구함
			int temp = Math.abs(Arrays.binarySearch(LIS, 0, size, arr[i]))-1;
			LIS[temp] = arr[i];
			
			// 뒤에 붙는 경우
			if(temp == size) {
				size++;
			}
		}
		System.out.println(size);
```

- 시간 복잡도
    - O ( N log N )

### [출처]

[https://source-sc.tistory.com/14](https://source-sc.tistory.com/14)