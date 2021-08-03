# LIS (Longest Increasing Subsequence) 최장 증가 수열 
```
210803 TIL #1
사용언어 : C언어 
```
## ✔️LIS 란?
어떠한 수열에서 오름차순으로 증가하는 **가장 긴 부분 수열**. 부분수열의 각 수는 **서로 연속할 필요는 없다.**

![LIS 이미지](https://blog.kakaocdn.net/dn/bdDSVs/btrbbScHFXx/l7rrP3GmqR3UM9HB8l7nQk/img.jpg)

***

## ✔️LIS 길이 구하기
: 가장 단순한 방법은 완전 탐색을 하는 것이다.

수열의 개수가 K개 -> 1개 이상의 원소를 갖는 부분 수열의 가짓수는 2^K
즉, 모든 부분 수열을 확인해 오름차순으로 정렬되어 있는지 확인하는 것은 매우 비효율적이다. 

이를 개선하기 위해 <span style="color:blue">다이나믹 프로그래밍</span>으로 구현 가능하다.

### ✔️#1 DP(Dynamic Programming)
```
시간 복잡도 : O(n^2)
```
수열의 한 원소(k)에 대해, 그 원소에서 끝내는 최장 증가 수열 길이를 저장한다.

=> k를 제외한 모든 원소는 k보다 작아야 한다.

 따라서 k의 앞 순서에 있는 모든 원소들 중 값이 k보다 작은 원소에 대해, 그 각각의 원소에서 끝나는 LIS의 길이를 알고 있다면 k의 LIS도 알 수 있다.

![DP](https://blog.kakaocdn.net/dn/brIvuW/btraZLe9352/6xWbqkt4d9xQ8LhfmzDujK/img.jpg)
```
arr[i] > arr[j]라면 dp[i] = max(dp[i], dp[j] + 1)
( dp[j] + 1 은 현재 원소를 포함한 LIS 길이를 의미한다.)
```
8 이전의 {1, 5, 4, 2, 3}의 수열 중 각 원소의 LIS
- 1에서 끝나는 LIS 길이 : 1 {1}
- 5에서 끝나는 LIS 길이 : 2 {1, 5}
- 4에서 끝나는 LIS 길이 : 2 {1, 4}
- 2에서 끝나는 LIS 길이 : 2 {1, 2}
- 3에서 끝나는 LIS 길이 : 3 {1, 2, 3}

=> 가장 긴 LIS 길이인 3에 현재 원소 8까지 더한 {1, 2, 3, 8}이 LIS가 된다.
즉, dp[i] = ‘i번째 인덱스에서 끝나는 최장 증가 수열의 길이’ 가 된다.

[코드]

```C
// LIS 알고리즘 #1 DP (시간복잡도 :O(n^2)
#include <stdio.h>
#include <stdlib.h>
#define MAX_SIZE 1001
#define MAX(X,Y) ((X) > (Y) ? (X) : (Y))

int arr[MAX_SIZE];
int dp[MAX_SIZE];

int main() {
	int n, i, j;
	int max = 0;

	scanf_s("%d", &n); // 수열의 크기

	for (i = 0; i < n; i++) {
		scanf_s("%d", &arr[i]);
	}

	for (i = 0; i < n; i++) {
		dp[i] = 1;
		for (j = 0; j < i; j++) {
			if (arr[i] > arr[j])
				dp[i] = MAX(dp[i], dp[j] + 1);
		}
	}

	for (i = 0; i < n; i++) {
		if (max < dp[i])
			max = dp[i];
	}

	printf("%d\n", max);
}
```
***

### ✔️#2 이분 탐색(binary search)
```
시간 복잡도 : O(NlogN)
```
DP를 이용한 방법은 완전 탐색에 비하면 시간 복잡도 면에서 효율적이지만 여전히 O(N^2)인 문제를 가지고 있다.

이제는 이분 탐색 방법을 이용해 LIS를 기록하는 배열을 하나 더 두고, 원래 수열에서의 각 원소에 대해 LIS 배열 내에서의 위치를 찾아보자.


![이분 탐색](https://blog.kakaocdn.net/dn/dFlw1O/btra33TSBcv/jTxkKUNL1xhfUaJKrc3B7K/img.jpg)

```
arr의 원소를 하나씩 확인하면서
0번째라면 lis[0] = arr[0];
```
- lis의 끝 원소보다 arr의 원소가 크다면?
    + lis의 끝에 추가 lis[++idx] = arr[i]

- lis의 끝 원소보다 arr의 원소가 작거나 같다면?
    + lis에서 적합한 위치를 찾아 원소를 교체 lis[lower_bound(0, idx, arr[i])] = arr[i]

=> 위치를 찾는 <span style="color:red">Lower Bound</span>를 알아야 한다.
***
### ❓ Lower Bound
```
정렬된 배열에서 찾고자 하는 값 이상이 처음으로 나타는 위치
```
![lower bound](https://blog.kakaocdn.net/dn/sSvGn/btra6HXkbv6/LXWMiHvB9oGpmWk3iGRTm1/img.jpg)

[코드]
```C
// LIS 알고리즘 #2 binary search (시간복잡도 :O(nlogn))
#include <stdio.h>
#include <stdlib.h>
#define MAX_SIZE 1000001

int lis[MAX_SIZE];

int lower_bound(int start, int end, int target) {
	int mid;

	while (start < end) {
		mid = (start + end) / 2;

		if (lis[mid] < target)
			start = mid + 1;
		else
			end = mid;
	}
	return start;
}
int main() {
	int n, i, ans;
	int lis_idx = 0;

	scanf_s("%d", &n); // 수열의 크기

	for (i = 0; i < n; i++) {
		scanf_s("%d", &ans);

		if (i == 0) lis[lis_idx] = ans;
		
		if (ans > lis[lis_idx])
			lis[++lis_idx] = ans;
		else
			lis[lower_bound(0, lis_idx, ans)] = ans;
	}
    printf("%d", lis_idx + 1);
}
```
***
### ❓ LIS 길이와 수열 모두 구하기
앞선 코드는 모두 길이를 구하는 알고리즘이다. 수열을 알기 위해서는 LIS 번호를 저장해야 한다.
```
각 원소 순서에 맞게 lis_idx를 저장한 후 역순으로 trace
```
![수열구하기](https://blog.kakaocdn.net/dn/BBig0/btraXWgZSrN/JGV4kyqveiiEIgMGkr0UCk/img.jpg)

위 예시에서 LIS의 길이는 3이다.
그러므로 temp 배열을 역순으로 trace 해보면서 LIS - 1부터 0까지 가장 처음으로 나온 원소들이 LIS에 해당함을 알 수 있다.

이때 주의할 점은 역순으로 trace하는 것이므로 배열에 저장할 때도 거꾸로 저장된다.

[코드]
```C
// LIS 알고리즘 #2 binary search (시간복잡도 :O(nlogn))
#include <stdio.h>
#include <stdlib.h>
#define MAX_SIZE 1000001

int lis[MAX_SIZE];
int arr[MAX_SIZE];
int temp[MAX_SIZE]; // 수열 LIS 자리를 저장함.
int rlt[MAX_SIZE];

int lower_bound(int start, int end, int target) {
	int mid;

	while (start < end) {
		mid = (start + end) / 2;

		if (lis[mid] < target)
			start = mid + 1;
		else
			end = mid;
	}
	return start;
}

int main() {
	int n, i, ans;
	int t;
	int lis_idx = 0;

	scanf_s("%d", &n); // 수열의 크기

	for (i = 0; i < n; i++) {
		scanf_s("%d", &arr[i]);

		if (i == 0) {
			lis[lis_idx] = arr[i];
			temp[i] = lis_idx;
		}

		if (arr[i] > lis[lis_idx]) {
			lis[++lis_idx] = arr[i];
			temp[i] = lis_idx;
		}
		else {
			int index = lower_bound(0, lis_idx, arr[i]);
			lis[index] = arr[i];
			temp[i] = index;
		}
	}
	//LIS 길이 출력
	printf("%d\n", lis_idx + 1);

	t = n - 1;
	i = 0;
	// temp에 저장된 번호를 역순으로 trace
	while (lis_idx >= 0) {
		if (temp[t] == lis_idx) {
			rlt[i++] = arr[t];
			lis_idx--;
		}
		t--;
	}

	for (t = i - 1; t >= 0; t--)
		printf("%d ", rlt[t]);
}
```