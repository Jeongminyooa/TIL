# Binary Search Tree (이진 검색 트리)
```
210809 TIL #7 binary search tree
사용언어 : C언어
```
## ✔️이진 검색 트리란?
탐색 작업을 효율적으로 하기 위한 이진 트리 자료구조
```
key(왼쪽 서브트리) <= key(루트 노드) <= key(오른쪽 서브트리)
```
:point_right: 왼쪽 자식 노드의 값이 부모 노드보다 더 작은 값을 가지고, 오른쪽 자식 노드의 값이 부모 노드보다 더 큰 값을 가지게 된다.
![image](https://user-images.githubusercontent.com/78305431/128639509-d021aec5-2f65-47ee-9ac7-0d68d60f6fef.png)

이진 탐색을 중위 순회하면 오름차순으로 정렬된 값을 얻을 수 있다.
***
## ✔️탐색 연산
트리의 루트 노드부터 순회하며 탐색해야 하는 값과 루트 노드의 값을 비교한다.
- 탐색 키가 루트보다 큰 경우 오른쪽 자식을 방문한다.
- 탐색 키가 루트보다 작은 경우 왼쪽 자식을 방문한다.
- 탐색 키가 루트와 같은 경우 탐색을 마친다.

:point_right: 방문한 노드가 NULL이 될 때까지 탐색 값을 찾지 못하면, 해당 트리에 탐색값이 없는 것으로 간주한다.
![image](https://user-images.githubusercontent.com/78305431/128639558-9876d96d-bae5-4ee2-a50b-32f7d8970389.png)
***
## ✔️삽입 연산
삽입 이전에 적절한 자리를 찾기 위해 탐색이 필요하다. NULL을 만나면 해당 위치에 삽입한다.

## ❓ 특정 노드를 삽입할 때 필요한 시간
해당 노드가 자리를 찾아가기 위해 비교를 몇번 해야 하는지(= 해당 트리의 높이가 얼마인지)에 비례한다.
![image](https://user-images.githubusercontent.com/78305431/128639616-1cc9d3c7-9b60-4aad-85af-21761ad911be.png)
- 최선 : O(logN)
- 최악 : O(N)
***
## ✔️삭제 연산
특정 노드를 삭제하고 싶을 때, 단순히 그 노드를 지운다고 끝이 아니다.
![image](https://user-images.githubusercontent.com/78305431/128639656-d5f11360-02d3-449c-9a59-5ad532dc0fba.png)
트리의 구조 체제가 깨지게 된다!

그러므로 삭제하고자 하는 값을 가진 노드가 무엇인지에 따라 총 3가지의 경우를 고려해야 한다.

#### Case 1. 단말 노드인 경우
:point_right: 그냥 삭제하면 된다.

#### Case 2. 자식이 1개인 노드인 경우
:point_right: 해당 노드를 삭제하고 서브 트리는 부모 노드에 붙여 준다.

#### Case 3. 자식이 2개인 노드인 경우
:point_right: 삭제한 자리에 `가장 비슷한 값을 가진 다른 노드`로 대체해주어야 한다.

```
<오른쪽 자식 트리 중에서 가장 작은 값을 가지는 노드>
                    또는 
<왼쪽 자식 트리 중에서 가장 큰 값을 가지는 노드>
```
***
[코드]
```C
// 이진 검색 트리
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
	int data;
	struct TreeNode* left, * right;
}TreeNode;

//탐색 : 순환
TreeNode* search_recursion(TreeNode* root, int key)
{
	if (root == NULL)
		return NULL;
	
	if (key == root->data)
		return root;
	else {
		if (key < root->data)
			return search(root->left, key);
		else
			return search(root->right, key);
	}
}

//탐색 : 반복
TreeNode* search_loop(TreeNode* node, int key)
{
	while (node != NULL) {
		if (key == node->data)
			return node;
		else if (key < node->data)
			node = node->left;
		else
			node = node->right;
	}
	return NULL;
}

//삽입
TreeNode* insert_node(TreeNode* node, int key) {
	if (node == NULL) {
		TreeNode* temp = (TreeNode*)malloc(sizeof(TreeNode));
		temp->data = key;
		temp->left = temp->right = NULL;
		return temp;
	}
	else {
		if (node->data < key)
			node->left = insert_node(node->left, key);
		else
			node->right = insert_node(node->right, key);
	}
	return node;
}

//삭제
TreeNode* delete_node(TreeNode* node, int key)
{
	if (node == NULL) return node;

	if (key < node->data)
		node->left = delete_node(node->left, key);
	else if (key > node->data)
		node->right = delete_node(node->right, key);
	else {
		if (node->left == NULL) {
			TreeNode* temp = node->right;
			free(node);
			return temp;
		}
		else if (node->right == NULL) {
			TreeNode* temp = node->left;
			free(node);
			return temp;
		}
		else {
			TreeNode* temp = min_value_node(node->right);
			node->data = temp->data;
			node->right = delete_node(node->right, node->data);
		}
	}
}

TreeNode* min_value_node(TreeNode* node)
{
	TreeNode* current = node;
	// 맨 왼쪽 단말 노드를 찾으러 내려감
	while (current->left != NULL)
		current = current->left;
	return current;
}
int main()
{
	TreeNode* root = NULL;
	TreeNode* tmp = NULL;
	root = insert_node(root, 30);
	root = insert_node(root, 20);
	root = insert_node(root, 10);
	root = insert_node(root, 40);
	root = insert_node(root, 50);
	root = insert_node(root, 60);
	
	if (search(root, 30) != NULL)
		printf("이진 탐색 트리에서 30을 발견함 \n");
	else
		printf("이진 탐색 트리에서 30을 발견못함 \n");
	return 0;
}
```