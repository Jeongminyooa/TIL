# Sort (정렬)
```
210807 TIL #5 sort
사용언어 : C언어
```
## ✔️선택 정렬
```
시간복잡도 : O(n^2)
```
0~n 까지의 원소 중 가장 큰 원소 또는 가장 작은 원소를 탐색하여 재배열
```C
for(int i = 0; i < SIZE; i ++) {
    maxidx = i;
    for(int j = i + 1; j < SIZE; j++) {
        if(arr[maxidx] < arr[j])
            maxidx = j;
    }
    swap(arr[i], arr[maxidx]);
}
```
***
## ✔️버블 정렬
```
시간복잡도 : O(n^2)
```
인접한 원소끼리 비교하여 재배열해나가는 과정
```C
for(int i  = 0; i < SIZE; i++) {
    for(int j = 0; j < SIZE - 1 - i; j++) {
        if (arr[j] > arr[j+1])
            swap(arr[j], arr[j+1]);
    }
}
```
***
## ✔️삽입 정렬
```
시간복잡도 : O(n^2)
```

:point_right:  위 세가지 기초 정렬은 시간면에서 효율적이지 못하다,
***
## ✔️합병 정렬
```
시간복잡도 : O(nlogn)
```
재귀적으로 수열을 나눠 정렬한 후 합치는 정렬 `분할정복법`
![image](https://user-images.githubusercontent.com/78305431/128597360-6aeec280-3513-4eef-937b-bea5141fd847.png)

```C
void merge(int A[], int p, int q, int r) {
	int i = p, j = q + 1, t = 0;
	int* temp = (int*)malloc(sizeof(int) * (r - p + 1));

	while (i <= q && j <= r) {
		if (A[i] < A[j]) temp[t++] = A[i++];
		else temp[t++] = A[j++];
	}
	while (i <= q) temp[t++] = A[i++];
	while (j <= r) temp[t++] = A[j++];

	t = 0;
	for (i = p; i <= r; i++) A[i] = temp[t++];

	free(temp);

}

void mergeSort(int A[], int p, int r) {
	if (p < r) {
		int q = (p + r) / 2;
		mergeSort(A, p, q);
		mergeSort(A, q + 1, r);
		merge(A, p, q, r);
	}
	return;
}
```
merge sort는 **stable sort**이다.

## ❓ Stable Sort 
우선 순위가 같은 원소들끼리는 원래의 순서를 따라가도록 하는 정렬 
![image](https://user-images.githubusercontent.com/78305431/128597459-35bb5cb6-9f90-4cfd-bc60-7076c9f278c4.png)
:point_right: merge sort에서는 해당 성질을 만족시키기 위해 같은 우선 순위를 가진 원소는 항상 앞 리스트 원소가 먼저 들어간다.
```C
//merge 함수내에 ..
while (i <= q && j <= r) {
		if (A[i] < A[j]) temp[t++] = A[i++];
		else temp[t++] = A[j++];
	}
```

## ❓ Stable Sort 응용
1. 파일 정렬 : 파일의 크기 -> 시간 순으로 정렬 가능
2. 2차원 좌표 : y 크기로 먼저 머지 소트 -> x 크기로 다시 머지 소트. x가 작은 순으로, x가 동일하면 y가 작은 순서
---

## ✔️퀵 정렬
거의 모든 정렬 알고리즘보다 빨라 각종 라이브러리 정렬에서 쓰인다. 단, 코테에서 STL을 못 쓰고 정렬을 직접 구현해야 할 경우, **절대 퀵소트를 사용하지 말고** 머지나 힙 소트를 사용하라.

```
시간복잡도 : O(nlogn)
--> 최악의 경우 O(n^2)
(오름 차순이거나 내림 차순으로 정렬되어 잇는 배열을 퀵 정렬할 경우)
```
![image](https://user-images.githubusercontent.com/78305431/128597547-20106d25-f65a-4988-9760-fbb7a938cf4c.png)
전체 리스트를 2개의 부분 리스트로 분할

pivot을 기준으로 비균등적 분할
(<---> mid를 정하는 것은 균등적 분할이라 함.)

```C
void quickSort(int A[], int p, int r)
{
    if(p < r> {
        // 피봇으로 비균등적 분할 -> 정렬
        int q = partition(A, p, r);
        quickSort(A, p, q - 1);
        quickSort(A, q + 1, r);
    })
}

int partition(int A[], int p, int r)
{
    int pivot = A[r]; //pivot을 마지막 원소로 정함.
    int i = p - 1, j = p;

    while(j < r) {
        if(A[j] > pivot) {
            swap(A, i, j);
            i++;
            j++;
        }
        else 
        j++;
    }
    swap(A, i, r);
    return (i + 1);
}