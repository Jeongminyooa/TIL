# DFS (깊이우선탐색)
```
210813 TIL #11 dfs
사용언어 : C언어
```
## ✔️ DFS(Depth First Search)란?
다차원 배열에서 각 칸을 방문할 때 **깊이를 우선으로 방문**하는 알고리즘

한 방향으로 갈 수 있을 때까지 갔다가 더 이상 갈 수 없게 되면 가장 가까운 갈림길로 돌아와서 이 곳으로부터 다른 방향으로 다시 탐색을 진행한다.
***

## ✔️ 스택을 이용한 구현
1. 시작하는 칸을 스택에 넣고 방문했다는 표시를 남긴다.
2. 스택에서 원소를 꺼내어 그 칸과 상하좌우로 인접한 칸에 대해 3번을 진행한다.
3. 해당 칸을 이전에 방문했다면 아무것도 하지 않고, 처음으로 방문했다면 방문했다는 표시를 남기고 스택에 삽입한다.
4. 스택이 빌 때까지 2번을 반복한다.

:point_right: 모든 칸이 스택에 1번씩 들어가므로 시간복잡도는 칸이 N개일 때 `O(N)`

**BFS에서 큐가 스택으로 바뀌면 DFS**

```C
void DFS(int n, int m) {
	int r, c;
	element e;

	vis[0][0] = 1; // 시작 위치를 방문했다고 표시함
	e.x = 0;
	e.y = 0;
	stack[top++] = e; // 큐에 푸쉬함

	while (top > 0) {
		element pop = stack[--top];

		for (int i = 0; i < 4; i++) {
			int nx = pop.x + dx[i];
			int ny = pop.y + dy[i];

			if (nx >= 0 && nx < n && ny >= 0 && ny < m ) {
				if (matrix[nx][ny] == 1 && !vis[nx][ny]) {
					e.x = nx;
					e.y = ny;
					stack[top++] = e;
					vis[nx][ny] = 1;
				}
			}
		}
	}
	return;
}
```
***
## ✔️ 인접 행렬
그래프에서 재귀적으로 구현이 가능하다. (묵시적 스택)
```C
void DFS(GraphType* g, int v) {
    int w;

    vis[v] = 1;
    printf("%d-> ", v);
    for(w = 0; w < g->n; w++) {
        if(!vis[w] && g->mat[v][w])
            DFS(g, w);
    }
}
```
***
## ✔️ 인접 리스트
그래프에서 재귀적으로 구현이 가능하다. (묵시적 스택)
```C
void DFS(GraphType* g, int v) {
    GraphNode* w;

    vis[v] = 1;
    printf("%d-> ", v);
    for(w = g->list[v]; w != NULL; w = w->link) {
        if(!vis[w->vertex])
            DFS(g, w->vertex);
    }
}
```
***
## ✔️ BFS vs DFS
둘은 스택과 큐라는 사용 자료구조의 차이가 있지만 알고리즘의 흐름은 같다. 하지만 둘의 방문 순서에는 큰 차이가 있다!
![image](https://user-images.githubusercontent.com/78305431/129372037-1a85a8dd-b91c-4b4c-94a8-567001a3bed3.png)

- BFS는 마치 냇가에 던진 돌로 인해 동심원이 생기는 것과 같다.
- DFS는 마치 미로 속에서 한 방향으로 막힐 때까지 직진하는 것과 같다.

BFS는 "현재 보는 칸으로부터 추가되는 인접한 칸은 거리가 현재 보는 칸보다 1만큼 떨어져 있다." 가 성립한다. 그러나 DFS에서는 성립하지 않는다. 그러므로 다차원 배열에서 순회하는 문제는 BFS를 사용해야 한다.