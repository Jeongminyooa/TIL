# Priority Queue (우선순위 큐)
```
210810 TIL #8 queue
사용언어 : C언어
```
## ✔️Priority Queue 란?
우선 순위를 가진 항목들을 저장하는 큐.

기존 큐 처럼 FIFO 형식이 아닌 우선순위가 높은 데이터가 먼저 나가게 된다.
- 최소 우선순위 큐
- 최대 우선순위 큐

:point_right: 스택이나 FIFO 큐로도 구현할 수 있다.
```
ex) 시뮬레이션 시스템, 네트워크 트래픽 제어, 운영체제에서의 작업 스케줄링 등.
```
*** 
## ❓ 구현 방법
![image](https://user-images.githubusercontent.com/78305431/128889387-0788fb98-70ff-441c-83a2-af9ee793a39b.png)
***

## ✔️ Heap 란?
노드의 키들이 다음 식들을 만족하는 <span style="color:red">**완전 이진 트리**</span>

### 종류
+ 최대 히프(max heap)
    - key(부모 노드) >= key(자식 노드)
    ![image](https://user-images.githubusercontent.com/78305431/128889770-32200997-d5ce-4074-8983-27ad549de19f.png)
+ 최소 히프(min heap)
    - key(부모 노드) <= key(자식 노드)
    ![image](https://user-images.githubusercontent.com/78305431/128889952-4d589427-8bbb-4b3d-b6e9-1f611ae46c16.png)


### 높이
n개의 노드를 가지고 있는 히프의 높이
```
O(logn)
```
:point_right: 완전 이진 트리

마지막 h 레벨을 제외하고는 각 레벨은 2^(h-1) 개의 노드가 존재한다.
![image](https://user-images.githubusercontent.com/78305431/128890238-54d9a24d-6d8e-45e0-a95f-7ad6f03ba37c.png)
***

## ✔️ Heap 구현
배열을 이용한 구현

완전 이진 트리이므로 각 노드에 번호를 붙일 수 있다. 그 번호를 인덱스로 생각하자.

![image](https://user-images.githubusercontent.com/78305431/128890518-2c30d98f-a808-4475-ac51-dbdf9982533a.png)

- 왼쪽 자식 인덱스 : 2i
- 오른쪽 자식 인덱스 : 2i + 1
- 부모 인덱스 : i / 2

### 삽입 
```
신입사원이 들어오면 일단 말단에 앉히고 능력을 봐서 위로 승진시키는 것과 비슷하다.
```
1. 히프에 새로운 요소가 들어오면, 일단 새로운 노드를 히프의 마지막 노드에 이어서 삽입한다.
2. 삽입 후에 새로운 노드를 부모 노드와 비교, 교환해서 히프의 성질을 만족한다.


### 삭제
```
사장의 빈 자리에 말단 사원이 올라가 능력에 따라 강등시키는 것과 비슷하다.
```
최대 히프에서의 삭제 = 가장 큰 키 값을 가진 노드륵 삭제 :point_right: 루트 노드 삭제

1. 루트 노드를 삭제한다.
2. 가장 마지막 노드를 루트 노드로 이동한다.
3. 루트부터 단말 노드까지의 경로에 있는 노드들을 교환하여 히프의 성질을 만족한다.

***

## ✔️ Heap 시간복잡도
```
O(logn)
```
- 삽입 : 최악의 경우, 루트 노드까지 올라가야 하므로 높이만큼 비교, 이동한다.
- 삭제 : 최악의 경우, 가장 아래 노드까지 내려가야 하므로 높이만큼 비교, 이동한다.

***
[코드]
```C
#include <stdio.h>
#include <stdlib.h>

#define MAX_ELEMENT 200

typedef struct {
	int key;
}element;

typedef struct {
	element heap[MAX_ELEMENT];
	int heap_size;
}HeapType;

HeapType* create()
{
	return (HeapType*)malloc(sizeof(HeapType));
}

void init(HeapType* h)
{
	h->heap_size = 0;
}

// 현재 요소의 개수가 heap_size인 히프 h에 item을 삽입한다.
// 삽입 함수
void insert_max_heap(HeapType* h, element item)
{
	int i;
	i = ++(h->heap_size);
	// 트리를 거슬러 올라가면서 부모 노드와 비교하는 과정
	while ((i != 1) && (item.key > h->heap[i / 2].key)) {
		h->heap[i] = h->heap[i / 2];
		i /= 2;
	}
	h->heap[i] = item; // 새로운 노드를 삽입
}

// 삭제 함수
element delete_max_heap(HeapType* h)
{
	int parent, child;
	element item, temp;
	item = h->heap[1];
	temp = h->heap[(h->heap_size)--];
	parent = 1;
	child = 2;
	while (child <= h->heap_size) {
		// 현재 노드의 자식노드 중 더 작은 자식노드를 찾는다.
		if ((child < h->heap_size) &&
			(h->heap[child].key) < h->heap[child + 1].key)
			child++;
		if (temp.key >= h->heap[child].key) break;
		// 한 단계 아래로 이동
		h->heap[parent] = h->heap[child];
		parent = child;
		child *= 2;
	}
	h->heap[parent] = temp;
	return item;
}

int main()
{
	element e1 = { 10 }, e2 = { 5 }, e3 = { 30 };
	element e4, e5, e6;
	HeapType* heap;

	heap = create(); // 히프 생성
	init(heap); // 초기화

	// 삽입
	insert_max_heap(heap, e1);
	insert_max_heap(heap, e2);
	insert_max_heap(heap, e3);

	// 삭제
	e4 = delete_max_heap(heap);
	printf("< %d > ", e4.key);
	e5 = delete_max_heap(heap);
	printf("< %d > ", e5.key);
	e6 = delete_max_heap(heap);
	printf("< %d > \n", e6.key);

	free(heap);
	return 0;
}
```
***
## ✔️ Heap Sort
1. 정렬해야 할 n 개의 요소들을 최대 히프에 삽입
2. 하나씩 삭제하고 별도 배열에 저장
3. 삭제되는 순서는 값이 증가되는 순서(최소 히프)
```
삽입과 삭제가 O(logn) + n개 요소 반복 O(n)
==> O(nlogn)
```
:point_right: 히프 정렬이 최고로 유용할 떄는 전체 자료 정렬이 아닌 **가장 큰 값 또는 가장 작은 값 몇개**만 필요한 경우이다.

[코드]
```C
//히프 정렬
#include <stdio.h>
#include <stdlib.h>
#define MAX_ELEMENT 200


/* 히프 구현 코드
...
*/

// 우선 순위 큐인 히프를 이용한 정렬
void heap_sort(element a[], int n)
{
	int i;
	HeapType* h;

	h = create();
	init(h);
	for (i = 0; i < n; i++) {
		insert_max_heap(h, a[i]);
	}
	for (i = (n - 1); i >= 0; i--) {
		a[i] = delete_max_heap(h);
	}
	free(h);
}

#define SIZE 8
int main(void)
{
	element list[SIZE] = { 23, 56, 11, 9, 56, 99, 27, 34 };
	heap_sort(list, SIZE);
	for (int i = 0; i < SIZE; i++)
	{
		printf("%d ", list[i].key);
	}
	printf("\n");
	return 0;
}
```
***

## ✔️ 머신 스케줄링(Machine Schedling)
공장에서 동일한 기계가 있고, 처리해야 하는 작업을 가지고 있을 때, 모든 기계가 풀동원하여 가장 최소의 시간 안에 작업들을 모두 끝내는 것

## ❓ LPI 알고리즘 (Longest Processing time First)
가장 긴 작업을 우선적으로 기계에 할당하는 방법
![image](https://user-images.githubusercontent.com/78305431/128914838-91502dee-7f19-4dc9-8507-61bf677f15e0.png)

[코드]
```C
// 히프를 이용한 머신 스케줄링
typedef struct {
	int id;
	int avail;
} element;
/* 히프 구현 코드
...
*/

#define JOBS 6
#define MACHINES 3

int main(void)
{
	int jobs[JOBS] = { 8, 7, 6, 5, 3, 2, 1 };    // 작업은 정렬되어 있다고 가정
	element m = { 0, 0 };
	HeapType* h;
	h = create();
	init(h);
	// 여기서 avail 값은 기계가 사용 가능하게 되는 시간 
	for (int i = 0; i < MACHINES; i++) {
		m.id = i + 1;
		m.avail = 0;
		insert_min_heap(h, m);
	}
	// 최소 히프에서 기계를 꺼내서 작업을 할당하고 사용가능 시간을 증가 시킨 후에 
	// 다시 최소 히프에 추가 
	for (int i = 0; i < JOBS; i++) {
		m = delete_min_heap(h);
		printf("JOB %d을 시간=%d부터 시간=%d까지 기계 %d번에 할당한다. \n",
			i, m.avail, m.avail + jobs[i] - 1, m.id);
		m.avail += jobs[i];
		insert_min_heap(h, m);
	}
	return 0;
}
```