# 컬렉션 (Collection)
```
210814 TIL #12 Collection
사용 언어 : JAVA
```
## ✔️ Java Collection FrameWork(JCF) 란?
Java에서 컬렉션이란 `데이터의 집합, 그룹`을 의미한다. JCF는 이러한 데이터, 자료구조인 컬렉션과 이를 구현하는 클래스를 정의하는 인터페이스(interface)를 제공한다. 이를 통해 다수의 데이터를 쉽고 효과적으로 처리할 수 있다.

배열이 가장 기본적인 자료구조이며, DTO 또한 자료를 담는 하나의 방식이라고 볼 수 있다.

## ❓ DTO (Date Transfer Object)
VO(Value Object)로 바꿔 말할 수 있는데 `계층 간 데이터 교환을 위한 자바 빈즈`를 말한다.

***

## ✔️ JCF 상속구조
![image](https://user-images.githubusercontent.com/78305431/129385734-5a97a2df-e3a1-4fcf-9443-83891b319e83.png)

Collection 인터페이스는 List, Set Queue로 크게 3가지 상위 인터페이스로 분류할 수 있다. Map의 경우 Collection 인터페이스를 상속받고 있지 않지만 Collection으로 분류된다.

***

## ✔️ Collection 인터페이스
컬렉션을 다루는데 가장 기본적인 동작들을 정의하고, 그것을 메소드로 제공하고 있다.

![image](https://user-images.githubusercontent.com/78305431/129388706-e1985323-5d69-4bd5-a086-340d62164091.png)

***

## ✔️ Collection 인터페이스 특징
### **List 인터페이스**
<span style="color:pink">순서가 있는</span> 데이터의 집합으로 데이터의 중복을 허용한다.

:point_right: <span style="color:pink">ArrayList는 Thread safe 하지 않고, Vector는 Thread safe하다.</span>

## ❓ Thread safe
멀티 스레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 혹은 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없음을 뜻한다.

구현 클래스
- Linked List
    + 양방향 포인터 구조로 데이터의 삽입, 삭제가 빈번할 경우 데이터의 위치 정보만 수정하면 되기에 유용하다.
    + 스택, 큐, 양방향 큐 등을 만들기 위한 용도로 쓰인다.
- Vector
    + 과거에 대용량 처리를 위해 사용했으며, 내부에서 자동으로 동기화 처리가 일어나 비교적 성능이 좋지 않고 무거워 잘 쓰이지 않는다.
- ArrayList
    + 단방향 포인터 구조로 각 데이터에 대한 인덱스를 가지고 있어 조회 기능에 성능이 뛰어나다.

***

### **Set 인터페이스**
순서를 유지하지 않는 데이터의 집합으로 데이터의 중복을 허용하지 않는다.

구현 클래스
- HashSet
    + 가장 빠른 임의 접근 속도
    + 순서를 예측할 수 없다.
- TreeSet
    + 정렬 방법을 지정할 수 있다.

***

### **Queue 인터페이스**
- List와 유사하며 먼저 들어온 데이터가 먼저 나가는 구조를 갖는다.

구현 클래스
- LinkedList
- PriorityQueue

***

### **Map 인터페이스**
키(Key)와 값(Value) 쌍으로 이루어진 데이터의 집합으로, 순서는 유지되지 않으며 키(Key)의 중복을 허용하지 않으나 값(Value)의 중복은 허용한다.

- Hashtable
    + HashMap 보다는 느리지만 동기화 지원
    + null 불가
- HashMap
    + 중복과 순서가 허용되지 않으며 null 값이 올 수 있다.
- TreeMap
    + 정렬된 순서대로 키와 값을 저장하여 검색이 빠르다.

## ❓ 배열과의 차이점
정적 메모리 할당이 아닌 동적 메모리 할당을 한다. 공간이 필요한 만큼 추가할 수 있다.
***

참고 - https://www.crocus.co.kr/1553

https://gangnam-americano.tistory.com/41

http://tcpschool.com/java/java_collectionFramework_concept