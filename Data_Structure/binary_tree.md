# Binary Tree (이진 트리)
```
210806 TIL #4 binary tree
사용언어 : C언어
```
## ✔️이진트리란?
모든 노드가 2개의 서브 트리를 가지고 있는 트리

💡 서브 트리는 공집합 일 수 있다.

![tree](https://user-images.githubusercontent.com/78305431/128484457-1ae58c5b-973f-4d96-875a-d981b9a785aa.png)
- 최대 2개까지의 자식 노드가 존재한다.
- 모든 노드의 차수가 2 이하이다. 구현이 편리하다.
- 서브 트리간의 순서가 존재한다.
***
## ✔️이진트리의 정의
1. 공집합도 이진 트리이다.
2. 서브 트리는 모두 이진 트리이어야 한다.
3. 루트와 왼쪽 서브 트리, 오른쪽 서브 트리로 구성된 노드들의 유한 집합이다.
***
## ✔️이진트리의 성질
- 노드의 개수가 **N** 이라면 간성의 개수는 **N-1** 이다.
- 높이가 **h** 라면 **최소 h개의 노드**를 가지고, **최대 2의 h승 - 1개의 노드**를 가진다.
![image](https://user-images.githubusercontent.com/78305431/128485054-4f22e6ca-8506-4cd4-a3b9-acdca957eeb3.png)
- n개의 노드를 가진 이진 트리의 높이는 최대 n의 높이를 가지고, 최소 log(n+1)의 높이를 가진다.
*** 
## ✔️이진트리의 분류
![image](https://user-images.githubusercontent.com/78305431/128485560-ecf56e9f-5c27-461a-bfba-c8073edaf239.png)
- 포화 이진 트리 (full binary tree)
- 완전 이진 트리 (complete binary tree)
- 기타 이진 트리 ex. 무한 완전 트리, 정 이진 트리, 균형 이진 트리, 변질 트리...

## ❓ 포화 이진 트리
트리 각 레벨에 노드가 꽉 차 있는 이진 트리

:point_right: 포화 이진 트리에서는 각 노드에 번호를 붙일 수 있다.

## ❓ 완전 이진 트리
레벨 1부터 K-1까지는 노드가 모두 채워져 있고 레벨 K에서는 왼쪽->오른쪽으로 노드가 순서대로 채워져 있는 이진트리 

:point_right: 포화 이진 트리와 노드 번호가 일치한다.
***
## ✔️ #1 배열표현법
모든 이진 트리를 포화 이진 트리라고 가정하고 각 노드에 번호를 붙여서 그 번호를 인덱스 삼아 노드의 데이터를 배열에 저장하는 방법
![image](https://user-images.githubusercontent.com/78305431/128486430-abef9133-3849-402f-b4f9-9b46da1449c8.png)
- 노드 i의 부모 인덱스 = i / 2
- 노드 i의 왼쪽 자식 인덱스 = 2n
- 노드 i의 오른쪽 자식 인덱스 = 2n + 1
***
## ✔️ #2 링크표현법
포인터를 이용하여 부모 노드가 자식 노드를 가리키게 하는 방법
![image](https://user-images.githubusercontent.com/78305431/128486652-5bdc2c5a-ec76-4763-a6c3-fd0ee8598af9.png)

```C
typedef struct TreeNode {
    int data;
    struct TreeNode * left, * right;
}TreeNode;
```
***
## ✔️이진트리의 순회 (traversal)
- 순회 : 트리의 노드들을 체계적으로 방문 :point_right: 재귀적 방법 사용
    + 전위순회 : VLR (루트 -> 자손)
    + 중위순회 : LVR (왼쪽 자손 -> 루트 -> 오른쪽 자손)
    + 후위순회 : LRV (자손 -> 루트)
## 1. 전위순회
1. 루트
2. 왼쪽 서브 트리
3. 오른쪽 서브 트리

ex) 목차

## 2. 중위순회
1. 왼쪽 서브 트리
2. 루트
3. 오른쪽 서브 트리

ex) 수식 트리

## ❓ 수식 트리 
산술식을 트리 형태로 표현한 것.
- 비단말 노드 :point_right: 연산자(operator)
- 단말 노드 :point_right: 피연산자(operand)
![image](https://user-images.githubusercontent.com/78305431/128490058-40c0cbb9-702c-48fe-9acb-d4abf940e8ea.png)
:point_right: 후위순회를 사용하여 서브트리의 값을 순환 호출로 계산할 수 있다. 비단말 노드를 방문할 때 양쪽 서브트리의 값을 노드에 저장된 연산자를 이용하여 계산한다.

## 코드
```C
// 수식 트리
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
	int data;
	struct TreeNode* left, * right;
}TreeNode;

int evaluate(TreeNode* p)
{
	if (p == NULL) return 0;
	if (p->left == NULL && p->right == NULL) return p->data;
	else {
		int op1 = evaluate(p->left);
		int op2 = evaluate(p->right);
		printf("%d %c %d을 계산합니다.\n", op1, p->data, op2);
		switch (p->data) {
		case '+': return op1 + op2;
		case '-': return op1 - op2;
		case '*': return op1 * op2;
		case '/': return op1 / op2;
		}
	}
	return 0;
}
// +
// * +
// 1 4 16 25
TreeNode n1 = { 1, NULL, NULL };
TreeNode n2 = { 4, NULL, NULL };
TreeNode n3 = { '*', &n1, &n2 };
TreeNode n4 = { 16, NULL, NULL };
TreeNode n5 = { 25, NULL, NULL };
TreeNode n6 = { '+', &n4, &n5 };
TreeNode n7 = { '+', &n3, &n6 };
TreeNode* exp = &n7;

int main(void)
{
	printf("수식의 값은 %d입니다. \n", evaluate(exp));
	return 0;
}
```

## 3. 후위순회 
1. 왼쪽 서브 트리
2. 오른쪽 서브 트리
3. 루트

ex) 디렉터리 용량 계산

## 코드
```C
//BOJ_1991
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
	char data;
	struct TreeNode* left, * right;
}TreeNode;

void preorder(TreeNode* root) {
	if (root != NULL) {
		printf("%c", root->data);
		preorder(root->left);
		preorder(root->right);
	}
	else return;
}

void inorder(TreeNode* root) {
	if (root != NULL) {
		inorder(root->left);
		printf("%c", root->data);
		inorder(root->right);
	}
	else return;
}

void postorder(TreeNode* root) {
	if (root != NULL) {
		postorder(root->left);
		postorder(root->right);
		printf("%c", root->data);
	}
	else return;
}

// 루트 노드부터 시작하여 target의 노드를 찾음(중위순회)
TreeNode* searchNode(TreeNode* root, char target) {
	if (root != NULL) {
		if (root->data == target) {
			return root;
		}
		TreeNode* tmp = searchNode(root->left, target);
		if (tmp != NULL)
			return tmp;

		return searchNode(root->right, target);
	}
	return NULL;
}

// parent 노드의 왼쪽, 오른쪽 자식 노드를 연결
void linkChild(TreeNode* parent, char ch1, char ch2)
{
	TreeNode* n1, * n2;

	if (ch1 == '.')	n1 = NULL;
	else {
		n1 = (TreeNode*)malloc(sizeof(TreeNode));
		n1->data = ch1;
		n1->left = NULL;
		n1->right = NULL;
	}

	if (ch2 == '.') n2 = NULL;
	else {
		n2 = (TreeNode*)malloc(sizeof(TreeNode));
		n2->data = ch2;
		n2->left = NULL;
		n2->right = NULL;
	}

	parent->left = n1;
	parent->right = n2;

	return;
}

int main()
{
	int n, i;
	char par, ch1, ch2;

	scanf_s("%d", &n); //노드의 개수 입력

	TreeNode* root = (TreeNode*)malloc(sizeof(TreeNode));
	root->data = 'A';
	root->left = NULL;
	root->right = NULL;

	i = n;
	while (i > 0) {
		scanf_s(" %c %c %c", &par, 1, &ch1, 1, &ch2, 1);
		getchar();

		TreeNode* p;
		
		if (i == n) p = root; //첫 입력이라면
		else p = searchNode(root, par); //노드를 찾아서 연결

		linkChild(p, ch1, ch2);

		i--;
	}

	preorder(root);
	printf("\n");
	inorder(root);
	printf("\n");
	postorder(root);

	return 0;
}
```

## 4. 반복 순회
스택을 이용해 반복으로 중위 순회를 할 수 있다.
![image](https://user-images.githubusercontent.com/78305431/128489048-ae29afce-ed93-4622-945c-96fcfbd618c4.png)
루프를 돌며
1. 해당 노드를 기준으로 가장 왼쪽 자손 노드로 이동하며 push
2. pop 해서 NULL이 아니면 출력
3. 오른쪽 노드로 이동
![image](https://user-images.githubusercontent.com/78305431/128488958-23cfe30d-f9ef-4041-a46b-e44379bb9dff.png)


## 코드
```C
// 스택과 반복을 이용한 중위순회
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
	int data;
	struct TreeNode* left, * right;
}TreeNode;

#define SIZE 100
int top = -1;
TreeNode* stack[SIZE];

void push(TreeNode* p)
{
	if (top < SIZE + 1) stack[++top] = p;
}

TreeNode* pop()
{
	if (top >= 0) return stack[top--];
}

void inorder_iter(TreeNode* root)
{
	while (1) {
		for (; root; root = root->left)
			push(root);
		root = pop();
		if (!root) break;
		printf("[%d] ", root->data);
		root = root->right;
	}
}
//		15
//	4		20
// 1	  16	25

TreeNode n1 = { 1, NULL, NULL };
TreeNode n2 = { 4, &n1, NULL };
TreeNode n3 = { 16, NULL, NULL };
TreeNode n4 = { 25, NULL, NULL };
TreeNode n5 = { 20, &n3, &n4 };
TreeNode n6 = { 15, &n2, &n5 };
TreeNode* root = &n6;

int main(void)
{
	printf("중위 순회=");
	inorder_iter(root);
	printf("\n");
	return 0;
}
```

## 5. 레벨 순회
큐를 이용해 각 노드를 레벨 순으로 검사하는 순회 방법이다.
![image](https://user-images.githubusercontent.com/78305431/128489048-ae29afce-ed93-4622-945c-96fcfbd618c4.png)
1. 루트 노드를 일단 큐에 삽입한다. `enqueue(root)`

큐가 empty될 때 까지

2. `dequeue` 출력
3. `enqueue(root->left) enqueue(root->right)`
![image](https://user-images.githubusercontent.com/78305431/128489587-f379e950-a5e3-4a2f-9a3c-516b2f5fa5d6.png)


## 코드

```C
// 큐를 이용한 레벨 순회
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
	int data;
	struct TreeNode* left, * right;
}TreeNode;

// 원형큐 코드
#define MAX_QUEUE_SIZE 100
typedef TreeNode* element;
typedef struct {
	element data[MAX_QUEUE_SIZE];
	int front, rear;
}QueueType;

void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

void init_queue(QueueType* q) {
	q->front = q->rear = 0;
}

int is_empty(QueueType* q)
{
	return q->front == q->rear;
}

int is_full(QueueType* q)
{
	return q->front == (q->rear + 1) % MAX_QUEUE_SIZE;
}

void enqueue(QueueType* q, element item)
{
	if (is_full(q))
		error("큐가 포화상태입니다.");
	q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;
	q->data[q->rear] = item;
}

TreeNode* dequeue(QueueType* q) 
{
	if (is_empty(q))
		error("큐가 공백상태입니다.");
	q->front = (q->front + 1) % MAX_QUEUE_SIZE;
	return q->data[q->front];
}

void level_order(TreeNode* ptr)
{
	QueueType q;

	init_queue(&q);
	enqueue(&q, ptr);

	while (!is_empty(&q)) {
		ptr = dequeue(&q);
		printf("[%d] ", ptr->data);
		if (ptr->left)
			enqueue(&q, ptr->left);
		if (ptr->right)
			enqueue(&q, ptr->right);
	}
}
// 15
// 4 20
// 1 16 25
TreeNode n1 = { 1, NULL, NULL };
TreeNode n2 = { 4, &n1, NULL };
TreeNode n3 = { 16, NULL, NULL };
TreeNode n4 = { 25, NULL, NULL };
TreeNode n5 = { 20, &n3, &n4 };
TreeNode n6 = { 15, &n2, &n5 };
TreeNode* root = &n6;
int main(void)
{
	printf("레벨 순회=");
	level_order(root);
	printf("\n");
	return 0;
}
```

</div>
</details>

***
## ✔️이진트리 연산
<details>
<summary>[코드]</sumarry>
<div markdown="1">

```C
#include <stdio.h>
#include <stdlib.h>
#define MIN(X,Y) ((X) < (Y) ? (X) : (Y))
#define MAX(X,Y) ((X) > (Y) ? (X) : (Y))

#define TRUE 1
#define FALSE 0
#define MAX_TREE_SIZE 20

typedef struct TreeNode {
	int data;
	struct TreeNode* left, *right;
}TreeNode;
/*
root	 15
	4			15
15			16		25
*/
TreeNode n1 = { 15, NULL, NULL };
TreeNode n2 = { 4, &n1, NULL };
TreeNode n3 = { 16, NULL, NULL };
TreeNode n4 = { 25, NULL, NULL };
TreeNode n5 = { 15, &n3, &n4 };
TreeNode n6 = { 15, &n2, &n5 };
TreeNode* root = &n6;

/*
root2	 15
	4			15
15			16		25
						28
*/
TreeNode m1 = { 15, NULL, NULL };
TreeNode m2 = { 4, &n1, NULL };
TreeNode m3 = { 16, NULL, NULL };
TreeNode m7 = { 28, NULL, NULL }; // 추가 
TreeNode m4 = { 25, NULL, &m7 }; // 변경 
TreeNode m5 = { 15, &m3, &m4 };
TreeNode m6 = { 15, &m2, &m5 };
TreeNode* root2 = &m6;

TreeNode* root3 = &n6;

//단말 노드 개수 계산
int get_leaf_count(TreeNode* t)
{
	if (t != NULL) {
		if (t->left == NULL && t->right == NULL)
			return 1;
		else {
			return get_leaf_count(t->left) + get_leaf_count(t->right);
		}
	}
	return 0;
}
// 비단말 노드 개수 계산
int get_noleaf_count(TreeNode* t)
{
	if (t != NULL) {
		if (t->left == NULL && t->right == NULL)
			return 0;
		else {
			return 1 + get_noleaf_count(t->left) + get_noleaf_count(t->right);
		}
	}
	return 0;
}

//자식이 하나인 비단말 노드의 개수
int get_oneleaf_count(TreeNode* t) {
	if (t != NULL) {
		if (t->left != NULL && t->right == NULL)
			return 1 + get_oneleaf_count(t->left);
		else if (t->left == NULL && t->right != NULL)
			return 1 + get_oneleaf_count(t->right);
		else {
			return get_oneleaf_count(t->left) + get_oneleaf_count(t->right);
		}
	}
	return 0;
}

//자식이 두개인 비단말 노드의 개수
int get_twoleaf_count(TreeNode* t) {
	if (t != NULL) {
		if (t->left != NULL && t->right != NULL)
			return 1 + get_twoleaf_count(t->left) + get_twoleaf_count(t->right);
		else {
			return get_twoleaf_count(t->left) + get_twoleaf_count(t->right);
		}
	}
	return 0;
}

//노드값 중 최대값을 반환
int get_max(TreeNode* t)
{
	int max = 0;

	if (t != NULL) {
		int lt = get_max(t->left);
		int rt = get_max(t->right);

		max = MAX(lt, rt);
		max = MAX(t->data, max);
	}
	return max;
}

//노드값 중 최솟값을 반환
int get_min(TreeNode* t)
{
	int min = 100;

	if (t != NULL) {
		int lt = get_min(t->left);
		int rt = get_min(t->right);

		min = MIN(lt, rt);
		min = MIN(t->data, min);
	}
	return min;
}

//트리에서 key값을 찾아 result에 주소값을 저장. 개수를 반환
int search(TreeNode* t, int key)
{
	if (t != NULL) {
		if (t->data == key) {
			return 1 + search(t->left, key) + search(t->right, key);
		}
		else 
			return search(t->left, key) + search(t->right, key);
	}
	return 0;
}

//이진 트리의 노드들의 값을 1씩 증가
void node_increase(TreeNode* t)
{
	if (t != NULL) {
		t->data++;
		node_increase(t->left);
		node_increase(t->right);
	}
	return;
}
void preorder(TreeNode* root) {
	if (root) {
		printf("%d ", root->data); // 노드 방문
		preorder(root->left); // 왼쪽서브트리 순회
		preorder(root->right); // 오른쪽서브트리 순회
	}
}

// 두 개의 이진 트리가 같은 구조를 갖고 있고 같은 데이터를 갖고 있는지 검사
int equal(TreeNode* r1, TreeNode* r2)
{
	if (r1 == NULL && r2 == NULL)
		return 1;
	if (r1 != NULL && r2 != NULL) {
		if (r1->data != r2->data) return 0;
		else {
			int le = equal(r1->left, r2->left);
			int re = equal(r1->right, r2->right);

			if (le == re) return 1;
		}
	}
	return 0;
}

// 주어진 이진 트리를 복제한 새로운 트리를 반환
TreeNode* copy(TreeNode* t)
{
	TreeNode* temp = (TreeNode*)malloc(sizeof(TreeNode));

	if (t != NULL) {
		temp->data = t->data;
		temp->left = copy(t->left);
		temp->right = copy(t->right);
		return temp;
	}
	return NULL;
}
int main()
{
	printf("root 트리의 연산 결과\n");

	printf("단말 노드 개수 : %d\n", get_leaf_count(root)); //3
	printf("비단말 노드 개수 : %d\n", get_noleaf_count(root)); // 3
	printf("자식이 하나만 있는 노드의 개수는 %d.\n", get_oneleaf_count(root)); //1
	printf("자식이 둘이 있는 노드의 개수는 %d.\n", get_twoleaf_count(root)); //2
	printf("최대값을 갖는 노드의 값은 %d\n", get_max(root)); //25
	printf("최소값을 갖는 노드의 값은 %d\n", get_min(root)); //4
	printf("15의 개수 = %d\n", search(root, 15));
	preorder(root);
	node_increase(root);
	preorder(root); // 1씩 증가하였는지 확인

	printf("\n-------------------------------------------\n");
	printf("root2 트리의 연산 결과\n");

	printf("단말 노드 개수 : %d\n", get_leaf_count(root2)); //3
	printf("비단말 노드 개수 : %d\n", get_noleaf_count(root2)); // 4
	printf("자식이 하나만 있는 노드의 개수는 %d.\n", get_oneleaf_count(root2));//2
	printf("자식이 둘이 있는 노드의 개수는 %d.\n", get_twoleaf_count(root2)); //2
	printf("최대값을 갖는 노드의 값은 %d\n", get_max(root2)); //28
	printf("최소값을 갖는 노드의 값은 %d\n", get_min(root2)); //4

	printf("\n-------------------------------------------\n");
	printf("root와 root2는 같은가? [ %d ]\n", equal(root, root2));
	printf("root와 root3는 같은가? [ %d ]\n", equal(root, root3));

	printf("root2를 복제한 후 1씩 더한 root4\n");
	TreeNode* root4 = copy(root2);
	node_increase(root4);
	preorder(root4);
	printf("\n\n원래의 root2\n");
	preorder(root2);
}
```

***
## ✔️스레드 이진 트리 (threaded binary tree)
이진 트리의 NULL 링크를 이용해 순환 호출 없이도 노드의 트리들을 순회

:point_right: NULL 링크에 중위 순회시에 후속 노드인 **중위 후속자(inorder successor)** 를 저장시켜놓은 트리
![image](https://user-images.githubusercontent.com/78305431/128491552-cb2126a3-ba82-437d-a641-b1a5b3579e18.png)

위 그림처럼 일반 이진 트리라면
- 총 링크의 개수 : 14개(2n)
- NULL이 아닌 링크 : 6개(n-1)
- NULL 링크 : 8개(n+1)

:point_right: 어차피 NULL 링크의 메모리는 할당되어 있기 때문에 **잉여 메모리를 활용하지 못하는 비효율성**을 모든 링크를 활용함으로써 해결할 수 있다. 중위 순회의 편의성이 증대된다.

## 코드
```C
// 스레드 이진 트리 코드
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
	int data;
	struct TreeNode* left, * right;
	int is_thread;
}TreeNode;

//p의 중위후속자를 찾는 함수
TreeNode* find_successor(TreeNode* p)
{
	TreeNode* q = p->right;

	if (q == NULL || p->is_thread)
		return q;

	while (q->left != NULL) q = q->left;
	return q;
}

void thread_inorder(TreeNode* t)
{
	TreeNode* q;
	q = t;
	while (q->left) q = q->left;
	do {
		printf("%c ", q->data);
		q = find_successor(q);
	} while (q);
}
// 7 
// 3 6 
// 1 2 4 5 
// 
TreeNode n1 = { '1', NULL, NULL, 1 }; // 단말 
TreeNode n2 = { '2', NULL, NULL, 1 }; // 단말 
TreeNode n3 = { '3', &n1, &n2, 0 };
TreeNode n4 = { '4', NULL, NULL, 1 }; // 단말 
TreeNode n5 = { '5', NULL, NULL, 0 }; // 단말이지만 중위 순회의 마지막 노드이므로 0으로 
TreeNode n6 = { '6', &n4, &n5, 0 };
TreeNode n7 = { '7', &n3, &n6, 0 };
TreeNode* exp = &n7;

int main()
{
	//단말 노드의 오른쪽 링크에 중위 후속 노드를 연결한다
	n1.right = &n3;
	n2.right = &n7;
	n4.right = &n6;

	thread_inorder(exp);
}
```