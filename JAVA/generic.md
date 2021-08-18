# 제네릭 (Generic)
```
210816 TIL #14 Generic
사용 언어 : JAVA
```
## ✔️ Generic 이란?
직역하자면 '일반적인' 이라는 뜻이다. 즉, `데이터 형식에 의존하지 않고, 하나의 값이 여러 다른 데이터 타입들을 가질 수 있도록 하는 방법`이다.

예를 들어, `ArrayList`, `LinkedList` 등을 생성 할 때
```java
//객체<타입> 객체명 new 객체<타입>();

ArrayList<Integer> list1 = new ArrayList<Integer>();
ArrayList<String> list2 = new ArrayList<Integer>();
 
LinkedList<Double> list3 = new LinkedList<Double>():
LinkedList<Character> list4 = new LinkedList<Character>();
```
이렇게 <> 괄호 안에 들어가는 타입을 지정해준다.

만약 우리가 어떤 자료구조를 만들어 배포하려 할 때 String 타입도 지원하고 싶고 Integer 타입도 지원하고 싶을 때 각각 따로 클래스를 만드는 것은 비효율적이기에 제네릭을 사용한다.

:point_right: **클래스 내부에서 특정(Specific) 타입을 미리 지정하는 것이 아닌 외부에서 사용자에 의해 지정되는 일반(Generic) 타입**이라는 것을 의미한다.
***
## ✔️ Generic의 장점
1. 제네릭을 사용하면 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지할 수 있다.
2. 클래스 외부에서 타입을 지정해주기 때문에 따로 타입을 체크하고 변환해줄 필요가 없다. 관리하기 편하다.
3. 비슷한 기능을 지원하는 경우 코드 재사용성이 높아진다.

***
## ✔️ Generic 사용 방법
보통 제네릭은 아래 표의 타입들이 많이 쓰인다.
<figure>
    <table>
        <thead>
            <tr>
                <td align="center" bgcolor="darkblue">타입</th>
                <td align="center" bgcolor="darkblue">설명</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>&lt;T&gt;</td>
                <td>Type</td>
            </tr>
            <tr>
                <td>&lt;E&gt;</td>
                <td>Element</td>          
            </tr>
            <tr>
                <td>&lt;K&gt;</td>
                <td>Key</td>
            </tr>
            <tr>
                <td>&lt;V&gt;</td>
                <td>Value</td> 
            </tr>
            <tr>
                <td>&lt;N&gt;</td>
                <td>Number</td> 
            </tr>
        </tbody>
    </table>
</figure>

:point_right: 반드시 한 글자일 필요는 없다. 또한 설명과 반드시 일치해야 할 필요도 없다. 예를 들어 <Ele> 라고 해도 전혀 무방하다. 다만 대중적으로 통하는 통상적인 선언이 가장 편하기 떄문에 암묵적인 규칙이 있을 뿐이다.
***
## ✔️ 클래스 및 인터페이스 선언
```java
public class ClassName <T> { ... }
public interface InterfaceName <T> { ... }
```
기본적으로 제네릭 타입의 클래스나 인터페이스는 위와 같이 선언한다. T 타입은 해당 블럭안에서까지 유효하다.

### ❓ 타입은 한 개뿐?
제네릭 타입은 두 개로 둘 수도 있다. 대표적으로 타입 인자를 두 개 받는 대표적인 컬렉션은 HasgMap이다.
```java
public class HashMap <V, K> { ... }
```

이렇게 생성된 제네릭 클래스를 사용하기 위해 객체를 생성할 때 구체적인 타입을 명시해준다.
```java
public class ClassName <T> { ... }

public class Main {
    public void static main(String[] args) {
        ClassName <String> ex1 = new ClassName<String>();
    }
}

```
이때 주의할 점은 **타입 파라미터로 명시할 수 있는 것은 참조 타입(Reference Type)밖에 올 수 없다.** 즉, int, double, char 같은 Primitice Type은 올 수 없다. 그래서 Wrapper Type으로 써야 한다.

바꿔 말하면 참조 타입이 올 수 있다는 것은 **사용자가 정의한 클래스도 타입으로 올 수 있다**는 것이다.
```java
public class ClassName <T> { ... }

public class Example { ... }

public class Main {
    public void static main(String[] args) {
        ClassName <Example> ex1 = new ClassName<Example>();
    }
}
```

제네릭 클래스를 사용하는 예시
```java
// 제네릭 클래스
class ClassName<E> {
	
	private E element;	// 제네릭 타입 변수
	
	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}
	
	E get() {	// 제네릭 타입 반환 메소드
		return element;
	}
	
}
 
class Main {
	public static void main(String[] args) {
		
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
		
		a.set("10");
		b.set(10);
	
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력 
		System.out.println("a E Type : " + a.get().getClass().getName());
		
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력 
		System.out.println("b E Type : " + b.get().getClass().getName());
		
	}
}
```
- a 객체의 ClassName의 E 제네릭 타입은 String으로 모두 변환된다.
- b 객체의 ClassName의 E 제네릭 타입은 Integer로 모두 변환된다.
***
## ✔️ 메소드 선언
클래스 내에서 사용할 수 있는 제네릭 타입 외에도 별도로 메소드에 한정한 제네릭도 사용할 수 있다.
```java
// 접근제어자 <제네릭 타입> 반환타입 메소드명(타입 파라미터)
public <T> void genericMethod(T o) {
    ...
}
```
클래스와 다르게 반환타입 이전에 <> 제네릭 타입을 선언한다.

제네릭 메소드까지 활용한 예제
```java
// 제네릭 클래스
class ClassName<E> {
	
	private E element;	// 제네릭 타입 변수
	
	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}
	
	E get() {	// 제네릭 타입 반환 메소드 
		return element;
	}
	
	<T> T genericMethod(T o) {	// 제네릭 메소드
		return o;
	}
 
	
}
 
public class Main {
	public static void main(String[] args) {
		
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
		
		a.set("10");
		b.set(10);
	
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력 
		System.out.println("a E Type : " + a.get().getClass().getName());
		
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력 
		System.out.println("b E Type : " + b.get().getClass().getName());
		System.out.println();
		
		// 제네릭 메소드 Integer
		System.out.println("<T> returnType : " + a.genericMethod(3).getClass().getName());
		
		// 제네릭 메소드 String
		System.out.println("<T> returnType : " + a.genericMethod("ABCD").getClass().getName());
		
		// 제네릭 메소드 ClassName b
		System.out.println("<T> returnType : " + a.genericMethod(b).getClass().getName());
	}
}
```
a 객체 또는 b 객체에 의해 타입이 결정되는 클래스와 다르게, **genericMethod()는 파라미터 타입에 따라 T 타입이 결정된다.**

:point_right: 클래스에 지정한 제네릭 타입과 별도로 메소드에서 독립적으로 제네릭 유형을 선언하여 쓸 수 있다.

### ❓ 제네릭 메소드는 왜 필요할까?
> 정적 메소드로 선언할 때 필요하기 때문이다.

앞서 제네릭은 타입을 외부에서 지정해준다고 했다. 즉 해당 클래스 객체가 인스턴스화 했을 때 타입이 지정된다는 것이다.

하지만 static은 기본적으로 프로그램 실행시 메모리에 이미 올라가 있다. 객체 생성을 통해 접근할 필요 없이 이미 메모리에 올라가 있기 때문에 클래스 이름을 통해 바로 사용할 수 있다는 것이다.

그렇다면 static 메소드는 객체 생성 전에 메모리에 올라가는데 타입을 어디서 얻어올 수 있을까?
```java
class ClassName<E> {
 
	/*
	 * 클래스와 같은 E 타입이더라도
	 * static 메소드는 객체가 생성되기 이전 시점에
	 * 메모리에 먼저 올라가기 때문에
	 * E 유형을 클래스로부터 얻어올 방법이 없다.
	 */
	static E genericMethod(E o) {	// error!
		return o;
	}
	
}
 
class Main {
 
	public static void main(String[] args) {
 
		// ClassName 객체가 생성되기 전에 접근할 수 있으나 유형을 지정할 방법이 없어 에러남
		ClassName.getnerMethod(3);
 
	}
}
```
:point_right: ***제네릭이 사용되는 메소드를 정적 메소드로 두고 싶은 경우 제네릭 클래스와 별도로 독립적인 제네릭이 사용되어야 한다***는 것이다.

```java
// 제네릭 클래스
class ClassName<E> {
 
	private E element; // 제네릭 타입 변수
 
	void set(E element) { // 제네릭 파라미터 메소드
		this.element = element;
	}
 
	E get() { // 제네릭 타입 반환 메소드
		return element;
	}
 
	// 아래 메소드의 E타입은 제네릭 클래스의 E타입과 다른 독립적인 타입이다.
	static <E> E genericMethod1(E o) { // 제네릭 메소드
		return o;
	}
 
	static <T> T genericMethod2(T o) { // 제네릭 메소드
		return o;
	}
 
}
 
public class Main {
	public static void main(String[] args) {
 
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
 
		a.set("10");
		b.set(10);
 
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력
		System.out.println("a E Type : " + a.get().getClass().getName());
 
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력
		System.out.println("b E Type : " + b.get().getClass().getName());
		System.out.println();
 
		// 제네릭 메소드1 Integer
		System.out.println("<E> returnType : " + ClassName.genericMethod1(3).getClass().getName());
 
		// 제네릭 메소드1 String
		System.out.println("<E> returnType : " + ClassName.genericMethod1("ABCD").getClass().getName());
 
		// 제네릭 메소드2 ClassName a
		System.out.println("<T> returnType : " + ClassName.genericMethod1(a).getClass().getName());
 
		// 제네릭 메소드2 Double
		System.out.println("<T> returnType : " + ClassName.genericMethod1(3.0).getClass().getName());
	}
}
```
***
## ✔️ 제한된 제네릭과 와일드 카드
지금까지의 제네릭은 가장 일반적인 예시로 참조 타입 모두 될 수 있다.

이떄 특정 범위 내로 좁혀서 제한하고 싶다면 `extends`와 `super` 그리고 `?`다.

- extends T : 상한 경계
- ? super T : 하한 경계
- <?> : 와일드 카드(Wild card)
```java
<K extends T>	// T와 T의 자손 타입만 가능 (K는 들어오는 타입으로 지정 됨)
<K super T>	// T와 T의 부모(조상) 타입만 가능 (K는 들어오는 타입으로 지정 됨)
 
<? extends T>	// T와 T의 자손 타입만 가능
<? super T>	// T와 T의 부모(조상) 타입만 가능
<?>		// 모든 타입 가능. <? extends Object>랑 같은 의미
```
`K extends T`와 `? extends T`는 비슷한 구조지만 차이점이 있다. **K는 특정 타입으로 지정되지만, ?는 타입이 지정되지 않는다는 의미다.**
```java
/*
 * Number와 이를 상속하는 Integer, Short, Double, Long 등의
 * 타입이 지정될 수 있으며, 객체 혹은 메소드를 호출 할 경우 K는
 * 지정된 타입으로 변환이 된다.
 */
<K extends Number>
 
 
/*
 * Number와 이를 상속하는 Integer, Short, Double, Long 등의
 * 타입이 지정될 수 있으며, 객체 혹은 메소드를 호출 할 경우 지정 되는 타입이 없어
 * 타입 참조를 할 수는 없다.
 */
<? extends T>	// T와 T의 자손 타입만 가능
```
:point_right: 특정 타입의 데이터를 조작하고자 할 경우 K 같이 특정 제네릭 인수로 지정해주어야 한다.
***
## ✔️ 제네릭 유형 제한 예시
1. &lt;K extends T>

제네릭 클래스에서 수를 표현하는 클래스만 받고 싶은 경우가 있다. 대표적인 `Integer, Long, Byte, Double, Float, Short` 같은 래퍼 클래스들은 `Number 클래스`를 상속 받는다.
```java
public class ClassName <K extends Number> {...}

public class Main {
	public static void main(String[] args) {
 
		ClassName<Double> a1 = new ClassName<Double>();	// OK!
 
		ClassName<String> a2 = new ClassName<String>();	// error!
	}
}
```
:point_right: 특정 타입 및 그 하위 타입만 제한하고 싶을 경우 쓸 수 있다. 만약 String을 파라미터로 넘겨줄 경우 Number 클래스와는 별개의 클래스이기 때문에 Bound mismatch 에러를 띄운다.

***

2. &lt;K super T>

해당 객체가 업캐스팅(Up Casting)이 될 필요가 있을 때 사용한다. 

예를 들어 Animal 클래스와 이를 상속받는 Kangaroo 클래스와 Horse 클래스가 있다고 가정해보자.

이 때 캥거루와 말은 종류가 다르지만, 둘 다 동물로 보고 자료를 조작해야할 수도 있다. 그럴 때 캥거루를 과일로 캐스팅 해야 하는데, 상위 타입으로 업 캐스팅이 필요하다. 이 때 `super`를 사용한다.

다른 예제로 제네릭 타입에 대한 객체비교가 있다.
```java
// 특정 제네릭에 대한 자기 참조 비교를 하고싶을 때
public class ClassName <E extends Comparable<? super E> { ... }
```
:point_right: **E 객체는 반드시 Comparable을 구현해야 한다**는 의미를 가진다.

> [Comparable과 Comparator](Comparable-Comparator.md)를 읽고 오면 수월한 이해가 가능하다.

```java
public class SoltClass <E extends Comparable<E>> { ... }
 
public class Student implements Comparable<Student> {
	@Override
	public int compareTo(Person o) { ... };
}
 
public class Main {
	public static void main(String[] args) {
		SoltClass<Student> a = new SoltClass<Student>();
	}
}
```
이렇게만 써도 무방하다. SoltClass의 E는 student가 되어야 하는데, Comparable<Person>의 하위 타입이어야 하므로 거꾸로 말해 Comparable을 구현해야한다는 의미이다. 그러면 왜 `Comparable<E>`가 아닌 `<? super E>` 일까?

```java
public class SoltClass <E extends Comparable<E>> { ... }	// Error가능성 있음
public class SoltClass <E extends Comparable<? super E> { ... }	// 안전성이 높음
 
public class Person {...}
 
public class Student extends Person implements Comparable<Person> {
	@Override
	public int compareTo(Person o) { ... };
}
 
public class Main {
	public static void main(String[] args) {
		SoltClass<Student> a = new SoltClass<Student>();
	}
}
```
만약 Person을 상속 받고 Comparable 구현에서 Person 타입으로 업캐스팅 한다면? a 객체는 타입 파라미터로 Student를 주지만 Comparable에서는 상위 타입을 비교하기 때문에 `<E extends Comparable<E>>`는 정렬이 안되거나 에러가 날 수 있다.

***
3. &lt;?>
<? extends Object> 와 마찬가지. Object는 자바에서의 모든 API 및 사용자 클래스의 최상위 타입이다.

즉, 묵시적으로 Object 클래스를 상속받는 것이나 다름 없다. 어떤 타입이든 상관이 없고 기능 사용에 관심이 있는 경우에 와일드 카드로 사용한다!

***
참고 - https://st-lab.tistory.com/153