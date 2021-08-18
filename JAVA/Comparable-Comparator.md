# Comparable과 Comparator
```
210816 TIL #14 Comparable and Comparator
사용 언어 : JAVA
```
## ✔️ Comparable과 Comparator란?
객체를 정렬하기 위해 사용한다.(정확히 말하면 그건 용도에 불과하다.) 
> 객체를 비교할 수 있도록 만든다.

Comparable과 Comparator는 모두 인터페이스이기 때문에 추상 메소드를 반드시 구현해야 한다. 

- **Comparable** 인터페이스에는 `compareTo(T o)` 메소드 하나가 선언되어 있다. 해당 인터페이스를 구현할 때 재정의가 필요하다.
- **Comparator** 인터페이스는 여러가지 메소드가 있지만 실질적으로는 `compare(T o1, T o2)` 메소드를 재정의해주어야 한다.

:point_right: Comparable 인터페이스를 쓰려면 compareTo 메소드를 구현해야하고, Comparator 인터페이스를 쓰려면 compre 메소드를 구현해야 한다.

### ❓ Comparator 메소드는 왜 모두 구현하지 않는가?
<details markdown="1">
<summary>내용 보기</summary>

인터페이스 내에 선언된 메소드를 '반드시 구현' 해야 한다했는데 왜 compare 메소드만 구현하는걸까?

인터페이스의 경우 메소드를 선언만 하고 함수 내용은 구체화하지 않는다.(추상 메소드)

자바8부터 인터페이스에서도 일반 메소드를 구현할 수 있도록 default 메소드와 static 메소드를 지원한다. default나 static으로 선언된 메소드는 기존 구현된 함수를 반환하거나 구현이 되어 있다. 

이 말은 default나 static으로 선언된 메소드가 아니면 추상 메소드 이므로 반드시 재정의해주어야 한다는 것이다.

```
static은 재정의 할 수 없고, default는 재정의할 수 있다.
```
</details>

***
## ✔️ 객체 비교
우리는 primitive 타입의 실수 변수(byye, int double 등)의 경우 기본 자료형이기 때문에 부등호를 갖고 쉽게 두 변수를 비교할 수 있다.
```java
if(a > b) {
	System.out.println("a가 b보다 큽니다.");
}
else if(a == b) {
	System.out.println("a와 b는 같습니다.");
}
else {
	System.out.println("b가 a보다 큽니다. ");
}
```
그렇다면 객체를 비교하기 위해서는 어떻게 해야할까? 일단 동물 클래스를 예제로 공부해보자.
```java
public class Animal {
    String name;
    int leg;

    public Animal(String name, int leg) {
        this.name = name;
        this.leg = leg;
    }
}

public class Main {
    public static void main(String[] args) {
        Animal horse = new Animal("Horse", 4);
        Animal kangaroo = new Animal("Kangaroo", 2);

        /*
        어떻게 비교할까?
        */
    }
}
```
이처럼 horse, kangaroo 두 객체를 생성했을 때 비교의 기준은 이름일지 다리의 개수일지 예측할 수 없다.

본질적으로 객체는 사용자가 기준을 정해주지 않은 이상 어떤 객체가 더 높은 우선 순위를 갖는지 판단할 수 없다. 그래서 이러한 문제를 해결하기 위해 Comparable과 Comparator가 쓰인다.
***
## ✔️ 차이점
1. Comparable은 `자기 자신과 매개 변수 객체를 비교` 하는 것이고, Comparator는 `두 매개변수 객체를 비교`한다는 것이다. 본질적으로 비교한다는 것 자체는 같지만, 비교 대상이 다르다.
2. Comparable은 `lang 패키지`에 있어서 import 해줄 필요가 없지만, Comparator는 `util 패키지`에 있어서 import 해주어야 한다.

***
## ✔️ Comparable
> 자기 자신과 매개변수 객체를 비교
```java
public interface Comparable<T> {
    int compareTo(T o) {
        ...
    }
}

public class Animal implements Comparable<T>> { 
 
/*
  code
 */
 
	// 필수 구현 부분
	@Override
	public int compareTo(T o) {
		/*
		 비교 구현
		 */
	}
}
```
Comparable 인터페이스를 구현해줄 때 **compareTo() 메소드를 재정의해주어 객체를 비교할 기준을 정의**해준다.

:point_right: Animal로 생성한 객체 자신과 매개변수 객체(Animal.copareTo(o);를 통해 들어온 파라미터 o)가 비교할 객체가 된다.

Animal 예제에 구체적으로 적용해보자
```java
public class Animal implements Comparable<T>> { 
 
    String name;
    int leg;
 
    public Animal(String name, int leg) {
        this.name = name;
        this.leg = leg;
    }

	// 필수 구현 부분
    @Override
	public int compareTo(T o) {
		/*
		 비교 구현
		 */
	}
}
```
만약 다리 개수를 기준으로 비교하자고 한다면 자기 자신의 `leg`와 매개변수로 들어온 o의 `leg`의 값을 비교하면 된다.
```java
// 필수 구현 부분
    @Override
	public int compareTo(T o) {
		if(this.leg > o.leg) {
            return 1;
        }
        else if(this.leg == o.leg) {
            return 0;
        }
        else {
            return -1;
        }
	}
```
:point_right: 값을 비교해서 정수를 반환한다. 

### ❓ 반환되는 정수의 값
조건문을 통해 대소비교를 할 때 자신과 차이가 얼마나 나느냐에 따라 값을 리턴한다. 
```
예를 들어 나보다 3이 크다면 3을 반환하고, 나보다 3만큼 작다면 -3을 반환한다. 나와 값이 같다면 차이가 없으므로 0을 반환한다.
```
정석적으로 대소비교에는 1, 0, -1 반환하는 방식을 사용한다.

그러나 그냥 두 비교대상의 값 차이를 반환해도 된다.
```java
// 필수 구현 부분
    @Override
	public int compareTo(T o) {
		return this.age - o.age;
	}
```
:point_right: 번거로운 조건식 없이 값의 차이에 따라 3개의 조건을 만족할 수 있다.

<details markdown="1">
<summary>Comparable 코드</summary>

this는 horse 객체 자신을 의미하고, o는 kangaroo 객체를 의미한다.

```java
public class Animal implements Comparable<T>> { 
 
    String name;
    int leg;
 
    public Animal(String name, int leg) {
        this.name = name;
        this.leg = leg;
    }

	// 필수 구현 부분
    @Override
	public int compareTo(T o) {
		return this.leg - o.leg;
	}
}

public class Main {
    public static void main(String[] args) {
        Animal horse = new Animal("Horse", 4);
        Animal kangaroo = new Animal("Kangaroo", 2);

        int isBig = horse.compareTo(kangaroo);
        if(isBig > 0) {
            System.out.println(horse.name + "말 " + kangaroo.name + "보다 다리 개수가 많다.");
        }
        else if(isBig == 0) {
            System.out.println(horse.name + "과(와) " + kangaroo.name + "는 다리 개수가 같다.");
        }
        else {
            System.out.println(horse.name + "은 " + kangaroo.name + "보다 다리 개수가 적다.");
        }
    }
}
```
</details>

### ❓ 주의점 : 비교 데이터 값의 범위
위에서 예시를 든 데이터 타입이 int형이므로 int형을 예로 들어 설명하겠다.

int 자료형은 32bit(4Byte) 자료형으로 표현 범위가 [-2^31 ~ 2^31-1] 으로, 이를 풀어쓰면 [-2,147,483,648 ~ 2,147,483,647] 이다. 만약 해당 범위 밖을 벗어나면 반대편의 값으로 넘어가게 된다. 
```
Overflow : 주어진 범위의 상한선을 넘다.
2,147,483,647 + 1 = 2,147,483,648 이어야 하지만 int 형에서는  표현할 수 없는 수로 int형의 최솟값 -2,147,483,648을 반환한다.

Underfolw : 주어진 범위의 하한선을 넘다.
 -2,147,483,648 - 1 = -2,147,483,649 이어야 하지만 int 형에서는 표현할 수 없는 수로 int형의 최댓값 2,147,483,647을 반환한다.
```
이러한 상황을 대비하기 위해서는 코드의 예시처럼 `return this.leg - o.leg;` 보다는 **<, >, ==으로 대소비교를 해주는 것이 안전하며 일반적으로 권장**되는 방식이다.
***
## ✔️ Comparator
> 두 매개변수 객체를 비교
```java
public interface Comparator<T> {
    int compare(T o1, T o2) {
        ...
    }
}

import java.util.Comparator;
public class Animal implements Comparator<T>> { 
 
/*
  code
 */
 
	// 필수 구현 부분
	@Override
	public int compare(T o1, T o2) {
		/*
		 비교 구현
		 */
	}
}
```
Comparator 인터페이스를 구현해줄 때 **compare() 메소드를 재정의해주어 객체를 비교할 기준을 정의**해준다.

:point_right: Animal로 생성한 두 객체를 비교해준다!

Animal 예제에 구체적으로 적용해보자
```java
public class Animal implements Comparator<T>> { 
 
    String name;
    int leg;
 
    public Animal(String name, int leg) {
        this.name = name;
        this.leg = leg;
    }

	// 필수 구현 부분
	@Override
	public int compare(T o1, T o2) {
		/*
		 비교 구현
		 */
	}
}
```
기본적으로 **compare 메소드 매커니즘 자체는 compareTo와 같다.
다만, 자기 자신과 비교되느냐 안되느냐의 차이**일 뿐이다.

```java
public class Animal implements Comparator<T>> { 
 
    String name;
    int leg;
 
    public Animal(String name, int leg) {
        this.name = name;
        this.leg = leg;
    }

	// 필수 구현 부분
	@Override
	public int compare(T o1, T o2) {
		if(o1.leg > o2.leg) {
            return 1;
        } 
        else if(o1.leg == o2.leg) {
            return 0;
        }
        else {
            return 1;
        }
        /*
        간략하게 표현하기
        return o1.leg - o2.leg;
        */
	}
}
```
Comparable의 compareTo는 선행 원소가 자기 자신이 되고, 후행 원소가 매개변수가 되는 반면에, Comparator의 compare는 선행 원소가 o1이 되고, 후행 원소가 o2가 된다.

즉, o1과 o2를 비교함에 있어 자기 자신은 두 객체 비교에 영향이 없다는 뜻이다.

<details markdown="1">
<summary>Comparator 코드</summary>

animal 객체와는 상관 없이 horse와 kangaroo 객체가 비교하여 값을 반환한다.

```java
import java.util.Comparator;
public class Animal implements Comparator<T>> { 
 
    String name;
    int leg;
 
    public Animal(String name, int leg) {
        this.name = name;
        this.leg = leg;
    }

	// 필수 구현 부분
    @Override
	public int compare(T o1, T o2) {
		return o1.leg - o2.leg;
	}
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Animal("Animal", 0);
        Animal horse = new Animal("Horse", 4);
        Animal kangaroo = new Animal("Kangaroo", 2);

        int isBig = animal.compare(horse, kangaroo);
        if(isBig > 0) {
            System.out.println(horse.name + "말 " + kangaroo.name + "보다 다리 개수가 많다.");
        }
        else if(isBig == 0) {
            System.out.println(horse.name + "과(와) " + kangaroo.name + "는 다리 개수가 같다.");
        }
        else {
            System.out.println(horse.name + "은 " + kangaroo.name + "보다 다리 개수가 적다.");
        }
    }
}
```
</details>

***
## ✔️ Comparator 활용
Comparator를 통해 compare 메소드를 사용하면 어떤 객체가 생성되든 비교를 하고 싶은 객체와는 상관이 없다. 단지 compare 메소드만 사용하면 되기 때문이다. :point_right: 일관성이 떨어진다.

```java
Animal rabbit = new Animal("Rabbit", 4);
Animal horse = new Animal("Horse", 4);
Animal kangaroo = new Animal("Kangaroo", 2);

int isBig;
isBig = rabbit.compare(rabbit, kangaroo);
isBig = horse.compare(horse, rabbit);
isBig = kangaroo.compare(kangaroo, horse);

```

비교만을 위해 Compare 객체를 하나 더 생성해주는 방법도 있다.
```java
Animal Compare = new Animal(" ", 0);
Animal horse = new Animal("Horse", 4);
Animal kangaroo = new Animal("Kangaroo", 2);

int isBig;
isBig = Compare.compare(rabbit, kangaroo);
isBig = Compare.compare(horse, rabbit);
isBig = Compare.compare(kangaroo, horse);
```
하지만 이 방법은 Animal 클래스에서의 변수들이 쓸모없이 생성되어 버린다는 단점이 있다. 그러므로 우리는 Coparator 기능만 따로 두고 사용하고 싶다. 이럴 때에는 **익명 객체(클래스)**를 활용한다.

### ❓ 익명 객체
이름이 정의되지 않은 객체를 의미한다. Java는 객체 지향 언어이다. 그렇기에 class를 생성해 객체의 이름을 정의한다. 하지만 특정 구현 부분만 따로 사용하거나, 부분적으로 기능을 일시적으로 바꿔야 할 경우 익명 객체를 사용하기도 한다.
```java
// Animal을 상속받은 새로운 class
Animal a = new Animal() { /* 구현 */ };
```
이름이 정의되어 있지 않기 때문에 특정 타입이 존재하는 것이 아니다. 그렇기에 익명 객체는 반드시 상속하는 대상이 있어야 한다. extends 뿐만 아니라 implements 또한 마찬가지다.

:point_right: Comparator도 인터페이스이기 때문에 구현할 대상이 존재하므로 익명 객체를 만들 수 있다!

```java
public class Main {
    public static void main(String[] args) {
        //지역 (non-static)
        Comparator<Animal> cmp = new Comparator<Animal>() {
            @Override
            public int compare(Animal o1, Animal o2) {
                return o1.leg - o2.leg;
            }
        };

        //전역 (static)
        public static Comparator<Animal> cmp = new Comparator<Animal>() {
            @Override
            public int compare(Animal o1, Animal o2) {
                return o1.leg - o2.leg;
            }
        };
    }
}
```
익명 객체를 사용하면 Animal 클래스 내부에서는 굳이 Comparator를 구현하지 않아도 된다. 외부에서 comp 객체로 생성됐기 떄문이다. 익명 객체는 여러 개 만들 수 있기 때문에 비교 기준이 달라진다면 또 다른 익명 객체를 만들어 주면 된다.

<details markdown="1">
<summary>Comparator 코드(익명 객체)</summary>


```java
import java.util.Comparator;
public class Animal { 
 
    String name;
    int leg;
 
    public Animal(String name, int leg) {
        this.name = name;
        this.leg = leg;
    }
}

public class Main {
    public static void main(String[] args) {
        Comparator<Animal> cmp = new Comparator<Animal>() {
            @Override
            public int compare(Animal o1, Animal o2) {
                return o1.leg - o2.leg;
            }
        };
        Animal horse = new Animal("Horse", 4);
        Animal kangaroo = new Animal("Kangaroo", 2);

        int isBig = cmp.compare(horse, kangaroo);
        if(isBig > 0) {
            System.out.println(horse.name + "말 " + kangaroo.name + "보다 다리 개수가 많다.");
        }
        else if(isBig == 0) {
            System.out.println(horse.name + "과(와) " + kangaroo.name + "는 다리 개수가 같다.");
        }
        else {
            System.out.println(horse.name + "은 " + kangaroo.name + "보다 다리 개수가 적다.");
        }
    }
}
```
</details>

***
참고 - https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html#method.summary

https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#method.summary

https://st-lab.tistory.com/243