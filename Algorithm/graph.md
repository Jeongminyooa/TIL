# Graph (그래프)
```
210810 TIL #10 graph
사용언어 : C언어
```
## ✔️ Graph 란?
연결되어 있는 객체간의 관계를 **점과 선으로 표현한** 자료구조
```
ex)
- 트리도 특수한 형태의 그래프
- 전기 회로의 소자 간 연결 상태
- 지도에서 도시들의 연결 상태
- 검색엔진에서 랭킹 산정하기
- 네비게이션 최단 경로 찾기
```
*** 
## ✔️ 그래프 역사
1800년대 오일러에 의해 창안되었다.

## ❓ 오일러 문제
모든 다리를 한번만 건너서 처음 출발했던 장소로 돌아오는 문제
![image](https://user-images.githubusercontent.com/78305431/129137119-38df7ea2-4e0a-4e51-b085-a75803711b51.png)
- A, B, C, D 지역의 연결관계 표현
    + 위치 : 정점
    + 다리 : 간선

![image](https://user-images.githubusercontent.com/78305431/129137221-aa83aa19-f05a-472a-93c9-1b09c15058ef.png)

오일러 정리
- 모든 정점에 연결된 간선의 수가 짝수이면 오일러 경로가 존재한다.

:point_right:  따라서 해당 그래프에는 오일러 경로가 존재하지 않는다.
***
## ✔️ 그래프 정의
그래프 G는 (V, E)로 표시

![image](https://user-images.githubusercontent.com/78305431/129137344-ab890774-791c-41b2-8099-f27792b124da.png)

- V = 여러가지 특성을 가질 수 있는 객체
- V(G) = 그래프 G의 정점들의 집합
- E = 정점들간의 관계
- E(G) = 그래프 G의 간선들의 집합

![image](https://user-images.githubusercontent.com/78305431/129138221-3ad7e45c-1b24-4fda-b1bf-0a5de8b9d944.png)
```
V(G1) = {0,1,2,3}
E(G1) = {(0,1), (0,3), (1,2), (2,3)}

V(G2) = {0,1,2,3}
E(G2) = {(0,1), (0,2)}

V(G3) = {0,1,2} 
E(G3) = {<0,1>, <1,0>, <1,2>}
```
---
## ✔️ 그래프의 종류

## ✔️ 네트워크(Network)
 = 가중치 그래프(Weighted Graph)

 간선에 비용(cost)이나 가중치(weight)가 할당된 그래프
 ```
 ex) 정점 : 도시 / 간선 : 도로 / 가중치 : 도로 길이
 ```
 ---
 ## ✔️ 부분 그래프(Subgraph)
 정점 집합 V(G)와 간선 집합 E(G)의 부분 집합으로 이루어진 그래프

 ![image](https://user-images.githubusercontent.com/78305431/129138571-6cb09edd-96b9-474f-9862-b993f4f61950.png)
 
 ---
 ### ✔️ **무방향 그래프(Undirected Graph)**
 그래프의 간선에 방향성이 없는 경우

![image](https://user-images.githubusercontent.com/78305431/129138687-9fa57149-a4f9-4078-a377-007d3dd073ed.png)

- 차수 (degree) : 하나의 정점에 연결된 다른 정점의 수
- 인접 정점(adjacent vertex) : 하나의 정점에서 간선에 의해 직접 연결된 정점

:point_right: 정점과 정점 사이에는 반드시 경로가 존재한다.

 ### ✔️ **방향 그래프(Directed Graph)**
 그래프의 간선에 방향성이 있는 경우
 ![image](https://user-images.githubusercontent.com/78305431/129138833-abe0c956-2077-440b-8fbf-583367cdfc4e.png)

 - 진출 차수(outdegree) : 외부로 나가는 간선의 수
 - 진입 차수(indegree) : 외부에서 들어오는 간선의 수
 
:point_right: 방향 그래프에서의 모든 간선의 수 = 진입차수의 합이다.

---

 ### ✔️ 사이클 (Cycle)
 단순 경로의 시작 정점과 종료 정점이 동일한 경로
 ### ❓ 단순 경로(Simple Path)
 경로 중에서 반복되는 간선이 없는 경로

 ![image](https://user-images.githubusercontent.com/78305431/129138912-4fbca792-005e-4935-a82f-b6882cb6f69a.png)

 ### ✔️ 그래프의 경로(Path)
 <span><img src="https://user-images.githubusercontent.com/78305431/129139054-2a16f734-8c9c-4fd2-8149-e125289802a0.png" width="200px" height="230px" title="경로" alt="RubberDuck"></img><br/></span>
 - 0, 1, 2, 3은 단순 경로 (O)
 - 0, 1, 3, 2는 단순 경로 (X)
 - 1, 0, 2, 3는 단순 경로 (O)
 - 1, 0, 2, 0는 단순 경로 (X)
 - 0, 1, 2, 0은 사이클 (O)

 ***
 ## ✔️ 그래프의 연결 정도
 
 ### 1. 연결 그래프(Connected graph)
 임의의 두 정점 사이에 항상 경로가 존재하는 그래프
 ![image](https://user-images.githubusercontent.com/78305431/129139538-fe0e9f62-309f-478e-bb90-bad02562a7e5.png)

### 2. 완전 그래프(Complete graph)
모든 정점이 연결되어 있는 그래프
```
n개의 정점을 가진 무방향 완전 그래프의 간선 수
n * (n - 1) / 2
```
![image](https://user-images.githubusercontent.com/78305431/129139640-35178c0d-d3f5-4e03-9eeb-31cfcae6e2c4.png)

 ### ❓ 간과하기 쉬운 그래프
 그래프는 꼭 연결되어 있을 필요도 없고, 두 정점 사이의 간선이 반드시 1개 이하일 필요도, 또 간선이 반드시 서로 다른 두 정점을 연결해야 할 필요도 없다.
 ![image](https://user-images.githubusercontent.com/78305431/129139771-5aa3e2c9-0e4f-4ab3-bb61-887242976e13.png)

 ### ✔️ 루프
 한 정점에서 시작해 같은 정점으로 들어오는 간선

 보통 문제에서는 필요에 따라 "그래프는 연결되어 있다/ 그래프는 연결 그래프이다.", "두 정점 사이의 간선은 최대 1개 존재한다./ 같은 간선은 한 번만 주어진다.", "간선의 두 정점은 서로 다르다."와 같이 조건을 엄밀하게 지정하는 경우가 많다.

 :point_right: 이러한 말이 없다면 **위와 같은 그래프의 형태**에 대해서도 정답이 나오도록 해야 한다.

 ### ✔️ 단순 그래프(Simple Graph)
 두 정점 사이의 간선이 1개 이하이고 루프가 존재하지 않는 그래프

 ***
## ✔️ 그래프 구현

### ✔️ 1. **인접 행렬(Adjacent Matrix)**
연결된 두 정점에는 1을, 연결되지 않은 두 정점에는 0을 넣어준다.
```
  if ( (i, j)가 그래프에 존재 ) 
    M[i][j] = 1;
```
- 무방향 그래프 
![image](https://user-images.githubusercontent.com/78305431/129140145-f8b668ef-a4a4-4314-b239-8a74e43e62c3.png)
 :point_right: 대각선을 두고 대칭

- 방향 그래프
![image](https://user-images.githubusercontent.com/78305431/129140182-d3d347dc-97c3-456d-9e1e-15cb11e62fe8.png)
 :point_right: 배열에서 (2,3)은 2에서 3으로 가는 간선이 있다는 의미

- 시간 복잡도
    + 두 점이 연결되어 있는지 O(1)
    + 모든 정점의 목록 O(V)

- 공간 복잡도
    + 가로, 세로 각각 V인 2차원 배열 O(V^2)
```C
//그래프 표현 #1 인접 행렬
#include <stdio.h>
#include <stdlib.h>

#define MAX_VERTICES 50
typedef struct GraphType {
	int v;
	int adj_mat[MAX_VERTICES][MAX_VERTICES];
}GraphType;

// 그래프 초기화
void init(GraphType* g)
{
	int r, c;
	g->v = 0;

	for (r = 0; r < MAX_VERTICES; r++)
		for (c = 0; c < MAX_VERTICES; c++)
			g->adj_mat[r][c] = 0;
}

//정점 삽입 연산
void insert_vertex(GraphType* g, int n)
{
	if ((g->v) + 1 > MAX_VERTICES) {
		printf("그래프: 정점의 개수 초과\n");
		return;
	}
	g->v++;
}

//간선 삽입 연산 (무방향 그래프)
void insert_edge(GraphType* g, int start, int end)
{
	if (start < 0 || start > g->v || end < 0 || end > g->v) {
		printf("그래프 : 정점 번호 오류\n");
		return;
	}
	g->adj_mat[start][end] = 1;
	g->adj_mat[end][start] = 1;
}

//간선 삽입 연산 (방향 그래프)
void insert_edge_directed(GraphType* g, int start, int end)
{
	if (start < 0 || start > g->v || end < 0 || end > g->v) {
		printf("그래프 : 정점 번호 오류\n");
		return;
	}
	g->adj_mat[start][end] = 1;
}

//간선 삭제 연산
void delete_edge(GraphType* g, int start, int end)
{
	if (start >= g->v || end >= g->n) {
		fprintf(stderr, "그래프: 정점 번호 오류");
		return;
	}

	g->adj_mat[start][end] = 0;
	g->adj_mat[end][start] = 0;
}

//차수를 계산하는 함수
int get_degree(GraphType* g, int v)
{
	int i, count = 0;

	for (i = 0; i < g->v; i++)
		if (g->adj_mat[v][i] == 1)
			count++;
	return count;
}
```
***
### ✔️ 2. **인접 리스트(Adjacency List)**
각 정점에 인접한 정점들을 연결리스트로 구현
![image](https://user-images.githubusercontent.com/78305431/129140877-b94a311d-25f0-4bed-b991-63f79434053f.png)
V개의 리스트를 만들어 각 리스트에 연결된 정점을 넣으면 된다.

- 삽입
    + 정점 u와 v의 간선 삽입![image](https://user-images.githubusercontent.com/78305431/129140999-178023a3-7e79-492b-a957-b694e0a1c74a.png)
    + 정점 u의 리스트에 정점 v라는 노드가 추가되어야 한다.
    + 정점 v 노드는 nodeU로 표현(u 리스트에 연결되니까)
    + nodeU는 **vertext = v / link = g->adj_list[u]** :point_right: u가 가리키던 것들을 연결
    + **g->adj_list[u] = nodeU**  :point_right: 다시 nodeU를 링크하면 리스트 완성

- 삭제
    + 정점 u와 v의 간선 삭제![image](https://user-images.githubusercontent.com/78305431/129141309-19ea358d-b6b2-4a95-939d-0bc294f03527.png)
    + 먼저 각 리스트에 정점을 찾아야 한다.
        * #1 리스트가 바로 가리키고 있는 경우![image](https://user-images.githubusercontent.com/78305431/129141406-dc975996-9058-4a2d-828b-10c82c618e92.png)
        * remove = *phead; :point_right: *phead는 u 리스트를 가리키는 이중 포인터
        * *phead = remove->link :point_right: 리스트는 다음 정점을 가리킨다.
        * free(remove) :point_right: 노드 삭제
        * #2 중간에 껴있는 경우
        * prevp = remove :point_right: 링크 연결을 위해 이전 노드를 저장해놓고 삭제할 노드를 찾음
        * 삭제할 노드를 찾았다면 prevp 링크를 remove 링크에 연결
```C
//그래프 표현 #2 인접 리스트 (무방향 그래프)
#include <stdio.h>
#include <stdlib.h>

#define MAX_VERTICES 50
typedef int element;
typedef struct GraphNode {
	int vertex;
	struct GraphNode* link;
}GraphNode;

typedef struct GraphType {
	int n;
	GraphNode* adj_list[MAX_VERTICES];
}GraphType;

void init(GraphType* g)
{
	int i;
	g->n = 0;

	for (i = 0; i < MAX_VERTICES; i++)
		g->adj_list[i] = NULL;
}

// 간선 삽입 연산(무방향), v를 u의 인접 리스트에 삽입한다.
void insert_edge(GraphType* g, int u, int v)
{
	//각 리스트에 연결될 노드
	GraphNode* nodeV, * nodeU;
	
	if (u >= g->n || v >= g->n) {
		fprintf(stderr, "그래프: 정점 번호 오류");
		return;
	}
	nodeU = (GraphNode*)malloc(sizeof(GraphNode));
	nodeU->vertex = v;
	nodeU->link = g->adj_list[u];
	g->adj_list[u] = nodeU;

	nodeV = (GraphNode*)malloc(sizeof(GraphNode));
	nodeV->vertex = v;
	nodeV->link = g->adj_list[v];
	g->adj_list[v] = nodeV;
}

// 간선 삭제 연산
void remove_node(GraphNode** phead, element item) { 
    GraphNode* p, * prevp;

    if (*phead == NULL)
        printf("리스트는 비어있습니다.\n");
    else if ((*phead)->vertex == item) {
        p = *phead;
        *phead = (*phead)->link;
        free(p);
    }
    else {
        p = *phead;
        do {
            prevp = p;
            p = p->link;
        } while (p != NULL && p->vertex != item);
        if (p != NULL) {
            prevp->link = p->link;
            free(p);
        }
        else
            printf("%d은 리스트에 없음\n", item);
    }
}
// 간선 삭제 연산, v를 u의 인접 리스트에서 삭제한다.
void delete_edge(GraphType* g, int u, int v)
{
    GraphNode* node;
    if (u >= g->n || v >= g->n) {
        fprintf(stderr, "그래프: 정점 번호 오류");
        return;
    }

    // 코드 삽입
    // (u, v)를 삭제한다. remove_node를 사용.
    remove_node(&g->adj_list[u], v);
    remove_node(&g->adj_list[v], u);
}
```

- 공간 복잡도 : O (V+E)
    + 무방향 그래프 : 리스트 V개 + 원소 1개당 간선 2개씩
    + 방향 그래프 : 리스트 V개 + 원소 1개당 간선 1개씩

:point_right: 인접 행렬과 비교했을 때 V가 크고 E가 상대적으로 작은 상황에서 공간을 절약할 수 있다. 또한 **코딩 테스트에서는 인접 행렬보다 훨씬 많이 사용하므로 반드시 익혀놓아야 한다.**

ex) V가 100,000이고 E가 200,000인 경우
- 인접 행렬 :point_right: 100,000 by 100,000 배열 필요 :point_right: 메모리 제한
- 인접 리스트 :point_right: 리스트 100,000개, 모든 리스트에 저장되는 원소의 총 합 200,000개 혹은 400,000개 :point_right: 문제없이 저장 가능

- 시간 복잡도 
    + 특정 정점과 연결된 정점 순회 :point_right: O(V)가 아닌 갯수만큼 `ex) 3과 연결된 정점 - 3번 리스트에서의 원소 개수`

---

## ✔️ 인접 행렬과 인접 리스트 비교
![image](https://user-images.githubusercontent.com/78305431/129142363-f199a951-e738-4390-83ae-d78746646ff4.png)

1. 임의의 두 정점이 연결되어 있는지를 확인하는 시간 복잡도
- 인접 행렬 : adj_matrix[u][v] 확인
- 인접 리스트 : 한 정점에 연결된 모든 정점 확인, 둘 중에서 차수가 작은 것을 택해서 확인

2. 한 정점에서 연결된 모든 정점을 확인하는 시간 복잡도
- 인접 행렬 : 1번부터 V번까지 확인
- 인접 리스트 : 자신과 연결된 관계만 확인

3. 효율적인 상황
```
ex) V가 100,000이고 E가 200,000
-> E가 V^2보다 훨씬 적으므로 인접 리스트가 효율적이다. 

V가 100이고 E가 7,000
-> 인접 행렬이 효율적
```
다만 일반적인 그래프 문제에서 "정점 u, v가 연결되어 있는지를 반복적으로 확인해야 하는 경우"는 거의 없다. 인접 행렬은 구현이 간단하다 외에는 이점이 없다!

---
참고 - https://baaaaaaaaaaaaaaaaaaaaaaarkingdog.tistory.com/