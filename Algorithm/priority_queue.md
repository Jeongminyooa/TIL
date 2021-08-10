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
노드의 키들이 다음 식들을 만족하는 **완전 이진 트리**

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