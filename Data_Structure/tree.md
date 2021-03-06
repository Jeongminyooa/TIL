# 트리(Tree)
```
210805 TIL #3 Tree
사용언어 : C언어 
```
## ✔️Tree 란?
**계층적인 구조**를 나타내는 자료구조

![tree](https://user-images.githubusercontent.com/78305431/128332577-39b75943-839d-412e-9f2e-2c06d3847961.png)

- 부모-자식 관계의 노드들로 이루어진다.
    + 디렉토리 구조, 결정 트리 등
***
## ✔️트리의 정의
수학적으로 정의하자면 
```
무방향이면서 사이클이 없는 연결 그래프
(undirected Acyclic Connected Graph)
```
- **V개**의 정점을 가진 트리는 **V-1개**의 간선을 갖고 있다.
- 임의의 두 점을 연결하는 simple path(= 정점이 중복해서 나오지 않을 경로)가 유일하다.

***
## ✔️트리의 용어
- **노드(node)** : 트리 구성 요소
- **루트(root)** : 부모가 없는 노드. 트리는 하나의 루트 노드만을 가진다.
- **서브트리(subtree)** : 하나의 노드와 그 노드의 자손들로 이루어진 트리
- **단말노드(leaf node, terminal node)** : 자식이 없는 노드
- **비단말노드** : 적어도 하나의 자식을 가지는 노드
- **자식, 부모, 형제, 조상, 자손 노드** : 인간의 개념과 같다.

![image](https://user-images.githubusercontent.com/78305431/128334734-6d7fbeac-279b-4f2c-b35f-6a227c5ba6e5.png)

- **레벨(level)** : 트리 각 층의 번호 (루트노드부터 1...)
- **높이(height)** : 트리의 최대 레벨. 루트 노드에서 가장 깊숙히 있는 노드의 깊이
- **차수(degree)** : 노드가 가지고 있는 자식 노드의 개수
- **깊이(depth)** : 루트 노드에서 각 노드까지 가는 경로의 길이
***
## ✔️트리의 성질
```
임의의 정점을 루트로 만들기
```
![image](https://user-images.githubusercontent.com/78305431/128334129-47994987-df46-43b7-a3e8-da5b9ae15422.png)

:point_right: 모두 같은 트리이다. 루트가 달라지면 각 노드의 부모도 달라진다. 
***
## ✔️트리의 종류
트리는 이진트리와 일반트리로 나누어진다.