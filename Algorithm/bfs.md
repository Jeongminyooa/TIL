# BFS (너비우선탐색)
```
210812 TIL #10 bfs
사용언어 : C언어
```
## ✔️ BFS(Breadth First Search)란?
다차원 배열에서 각 칸을 방문할 때 **너비를 우선으로 방문**하는 알고리즘

시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법.
***

## ✔️ 큐를 이용한 구현
![image](https://user-images.githubusercontent.com/78305431/129214599-cbffb7b8-7c69-4a3b-87ed-47eda9710343.png)
1. 시작하는 칸을 큐에 넣고 방문했다는 표시를 남긴다.
2. 큐에서 원소를 꺼내어 그 칸에 상하좌우로 인접한 칸에 대해 3번을 진행한다.
3. 해당 칸을 이전에 방문했다면 아무것도 하지 않고, 처음으로 방문했다면 표시를 남기고 해당 칸을 큐에 삽입한다.
4. 큐가 빌 때까지 2번을 반복한다.

:point_right: 모든 칸이 큐에 1번씩 들어가므로 칸이 N개일 때 `O(N)`

***
## ✔️ 인접 행렬
```C
int queue[10001];
int vis[10001];

void BFS_mat(GraphType* g, int v) {
    vis[v] = 1; //방문 표시
    queue[rear++] = v;
    printf("%d", v);
    while(first < rear) {
        int pop = queue[++front];
        for(int i = 1; i <= g->n; i++) {
            if(!vis[i] && g->adj_matrix[pop][i]) {
                vis[i] = 1;
                queue[++rear] = i;
                printf("%d", i);
            }
        }
    }
}
```
***
## ✔️ 인접 리스트
```C
void bfs_list(GraphType* g, int v)
{
    GraphNode* w;
    QueueType q;
    init(&q); // 큐 초기 화
    visited[v] = TRUE; // 정점 v 방문 표시
    printf("%d 방문 -> ", v);
    enqueue(&q, v); // 시작정점을 큐 저장
    while (!is_empty(&q)) {
        v = dequeue(&q); // 큐에 저장된 정점 선택
        for (w = g->adj_list[v]; w; w = w->link) //인접 정점 탐색
        if (!visited[w->vertex]) { // 미방문 정점 탐색
            visited[w->vertex] = TRUE; // 방문 표시
            printf("%d 방문 -> ", w->vextex);
            enqueue(&q, w->vertex); //정점을 큐에 삽입
        }
    }
}
```
***
## ✔️ BFS 시간복잡도
인접 행렬 `O(n^2)`

인접 리스트 `O(n+e)`