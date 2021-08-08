# Queue (큐)
```
210808 TIL #6 queue
사용언어 : C언어
```
## ✔️Queue 란?
한쪽 끝에서 원소를 넣고 반대쪽 끝에서 원소를 뺼 수 있는 자료구조.

**선입선출 FIFO (First In First Out)**

![image](https://user-images.githubusercontent.com/78305431/128633241-4254e303-dae9-4277-bdf2-ab7214395dba.png)

## ✔️원소의 삽입, 제거, 확인
```
시간복잡도 O(1)
```
원소의 추가, 제거, 제일 앞/뒤 원소 확인이 가능하다.\

- front는 가장 맨 앞 인덱스를 가리킨다 :point_right: pop할 떄 front를 증가
- rear은 가장 마지막 원소의 인덱스 + 1을 가리킨다 :point_right: push할 때 rear 증가

***
[코드]
```C
//BOJ_10845
#include <stdio.h>

#define MAX_SIZE 10001
int queue[MAX_SIZE];
int rear, head;

void init() {
	head = rear = 0;
}

int empty() {
	if (head == rear)
		return 1;
	else
		return 0;
}
//정수 x를 큐에 넣는 연산
void push(int x) {
	queue[rear++] = x;
}

// 가장 맨 앞 원소를 빼고, 출력
int pop() {
	if (empty())
		return -1;
	return queue[head++];
}

int size() {
	return rear - head;
}

int front() {
	if (empty()) return -1;
	else return queue[head];
}

int back() {
	if (empty())
		return -1;
	else
		return queue[rear - 1];
}

int main(void) {
    int n;
    char command[10];

    scanf_s("%d", &n); //주어지는 명령의 수

    init();

    while (n > 0) {
        n--;

        scanf_s("%s", command, 10);

        if (strcmp(command, "push") == 0) {
            int num;
            scanf_s("%d", &num);
            push(num);
        }
        else if (strcmp(command, "pop") == 0) {
            printf("%d\n", pop());
        }
        else if (strcmp(command, "size") == 0) {
            printf("%d\n", size());
        }
        else if (strcmp(command, "empty") == 0) {
            printf("%d\n", empty());
        }
        else if (strcmp(command, "front") == 0) {
            printf("%d\n", front());
        }
        else if (strcmp(command, "back") == 0) {
            printf("%d\n", back());
        }
    }
}
```
***
## ✔️Circular Queue 란?
관념적으로 배열이 원형인 것으로 front나 rear가 MAX -> 0으로 다시 오도록 한다.

![image](https://user-images.githubusercontent.com/78305431/128634379-84848327-6cc4-4f0c-b5f3-e6d83a726650.png)

[코드]
```C
#include <stdio.h>
#include <stdlib.h>
typedef struct {
	int* queue;
	int rear, head;
	int size;
}circleQueue;

void init(circleQueue* q, int n) {
	q->queue = (int*)malloc(sizeof(int) * n);
	q->size = n;
	q->rear = q->head = 0;
}

void enqueue(circleQueue* q, int x) {
	q->rear = (q->rear + 1) % q->size;
	q->queue[q->rear] = x;
}

int dequeue(circleQueue* q) {
	q->head = (q->head + 1) % q->size;
	return q->queue[q->head];
}

void removeHead(circleQueue* q) {
	q->head = (q->head + 1) % q->size;
}

int empty(circleQueue* q) {
	if (q->rear == q->head)
		return 1;
	else return 0;
}

int full(circleQueue* q) {
	if ((q->rear + 1) % q->size == q->head)
		return 1;
	else return 0;
}
```
***
## ✔️Deque 이란?
양쪽 끝에서 삽입과 삭제가 가능한 Double Ended Queue
![image](https://user-images.githubusercontent.com/78305431/128634515-1b3f0155-3fd2-4981-9846-e39ad02706a6.png)

***

## ✔️원소의 삽입, 제거, 확인
```
시간복잡도 O(1)
```
head와 tail의 초기값이 0이 아닌 MAX_SIZE / 2

:point_right: 원소의 추가/삭제가 양방향으로 이루어지므로 배열의 중간이 초기값으로 적절하다.

[코드]
```C
#include <stdio.h>
#include <stdlib.h>
typedef struct {
	int* deque;
	int rear, head;
}Deque;

void init(Deque* q) {
	q->deque = (int*)malloc(sizeof(int) * n);
	q->rear = q->head = MAX_SIZE / 2;
}

void push_front(Deque* q, int data) {
    q->deque[--head] = data;
}

void push_back(Deque* q, int data) {
    q->deque[rear++] = data;
}

int pop_front(Deque* q) {
    return q->deque[head++];
}

int pop_back(Deque* q) {
    return q->deque[--tail];
}

int size(Deque *q) {
    return rear - head;
}

int empty(circleQueue* q) {
	if (q->rear == q->head)
		return 1;
	else return 0;
}

int front (Deque* q) {
    if(empty(q))
        printf("덱이 비어 있습니다.\n");
    else
        return q->deque[head];
}

int back (Deque* q) {
    if(empty(q))
        printf("덱이 비어 있습니다.\n");
    else
        return q->deque[tail - 1];
}
```