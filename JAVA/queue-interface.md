# 큐 인터페이스 (Queue Interface)
```
210816 TIL #14 Queue Interface
사용 언어 : JAVA
```
## ✔️ Queue Interface
> 이 글을 읽기 전 [ [JAVA Collection이란?](collection.md) + [Queue 개념 정리](../Algorithm/queue.md) + [Generic에 대한 이해](generic.md)] 을 먼저 공부하고 오면 이해가 수월하다.

Java의 Queue Interface는 자료구조 큐를 약속한 것이다. 큐는 **FIFO 형태로 자료를 보관하고 꺼내는 버퍼**이다. 

***
## ✔️ 선언 메소드
Java의 Queue 인터페이스에서는 보관할 떄 offer 메소드를 사용하며 가장 먼저 보관한 자료를 꺼낼 때는 poll 메소드를 사용한다. 이 외에 가장 먼저 보관한 자료를 단순 참조하는 peek 메소드와 비었는지 판별하는 empty 메소드를 제공하고 있다.

<figure>
    <table>
        <thead>
            <tr>
                <td align="center" bgcolor="darkblue">메소드</th>
                <td align="center" bgcolor="darkblue">리턴 타입</th>
                <td align="center" bgcolor="darkblue">설명</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td >offer(E e)</td>
                <td>boolean</td>
                <td>- 큐의 마지막에 요소를 추가한다.<br> - 요소를 이 큐에 추가 가능한 경우는 true, 그렇지 않은 경우는 false</td>
            </tr>
            <tr>
                <td>poll()</td>
                <td>Element</td>
                <td>- 큐의 첫 번쨰 요소를 제거하고 제거된 요소를 반환한다. <br>- 큐가 비어있는 경우는 null</td>
            </tr>
            <tr>
                <td>peek()</td>
                <td>Element</td>
                <td>- 큐의 첫 번째 요소를 제거하지 않고 반환한다.<br>- 큐가 비어있는 경우는 null</td>
            </tr>
            <tr>
                <td>empty()</td>
                <td>boolean</td>
                <td>큐가 비어있는지 판별한다.</td>
            </tr>
        </tbody>
    </table>
</figure>

:point_right: 예외인 경우 null 또는 false의 값을 던진다.

그리고 제네릭 형태로 사용할 때 큐를 구현한 클래스인 `LinkedList, priorityQueue, priorityBlockingQueue`를 생성하여 사용한다.
***
## ✔️ 연결리스트를 이용한 큐
다음은 LinkedList를 생성하여 큐를 사용하는 예제이다.
```java
import java.util.Queue;
import java.util.LinkedList;

public class Practice {
    public static void main(String[] args) {
        Queue<String> q = new LinkedList<String>();
        q.offer("유정민");
        q.offer("너구리");
        q.offer("김또깡"); // "유정민""너구리""김또깡"

        System.out.println(q.peek()); //"유정민" 참조
        //여전히 "유정민""너구리""김또깡"

        System.out.println(q.poll()); //"유정민" 꺼냄
        //"너구리""김또깡"
        q.offer("유정민2"); //"너구리""김또깡""유정민2"
        while(!q.isEmpty()) {
            System.out.println(q.poll()); // "너구리""김또깡""유정민2" 순으로 출력
        }

    }
}
```
***
참고 - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#

https://st-lab.tistory.com/184?category=856997

http://cris.joongbu.ac.kr/course/java/api/java/util/Queue.html