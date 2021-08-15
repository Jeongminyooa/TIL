# Interface와 Abstract Class
```
210815 TIL #13 인터페이스 vs 추상 클래스
사용 언어 : JAVA
```
## ✔️ 인터페이스 추상클래스 왜 사용할까?
JAVA에서 추상 클래스와 인터페이스는 흔히들 들어보았을 것이다. 그러나 이론적인 내용 말고 정작 `"왜 사용하나요?", "차이점이 뭔가요?", "추상 클래스를 사용할지 인터페이스를 사용할지 어떻게 정하나요?"`와 같이 실무적인 질문이 들어오면 대답하기가 힘들 것이다.

 > **그것이 바로 나**이기 때문에 오늘의 TIL 주제는 인터페이스와 추상클래스 이다!

***

 ## ✔️ 추상 클래스란?
 일반적으로 Java에서 클래스는 **일반 클래스와 추상 클래스** 2가지로 구분된다. 
 추상 클래스는 일반 클래스와 별 다를 것이 없다. 단지, 추상 메소드를 선언하여 `상속을 통해서 자손 클래스에서 완성하도록 유도`하는 클래스이다. 그래서 **미완성 설계도**라고도 표현한다. 

 추상 클래스는 **필드, 생성자, 추상 메소드**를 가질 수 있다. 생성자를 가지기 때문에 객체화가 가능하며 인터페이스와 다르게 필드도 가질 수 있다. 

 추상 클래스는 추상 메소드를 꼭 가져야만 하는 것은 아니다. 단 `추상 메소드를 하나라도 가지는 클래스는 추상 클래스이다.`라고 할 수 있다. **상속을 위한 클래스이기 때문에 따로 객체를 생성할 수 없다.** 
 
 단, `상속(extends)`을 받은 하위 클래스는 객체화가 가능하다. 하위 클래스의 생성자에서 `super()` 변수를 사용해서 추상 클래스의 생성자를 부르고 초기화 시킨다.

선언 시 `abstarct` 예약어를 사용해 상속을 통해 구현해야함을 알려준다.

 ```java
abstract class 클래스 이름 {
    ...
    public abstract void 메서드 이름();
}
 ```

***
## ✔️ 인터페이스란?
추상 클래스가 미완성 설계도라면 인터페이스는 **기본 설계도**라고 할 수 있다. 추상 클래스처럼 다른 클래스를 작성하는데 도움을 주는 목적으로 작성하고 클래스와 다르게 `다중상속(구현)을 지원하며, 구현체에 여러개의 인터페이스를 구현할 수 있다.`

### ❓ 구현체
인터페이스를 구현한 클래스라는 뜻이며, 구현 클래스 혹은 실체 클래스 라고도 부른다.

인터페이스란 **상수와 추상 메소드의 집합**이다. `모든 메소드가 추상 메소드이고, 일반 변수를 가질 수 없다.` 생성자를 가질 수 없으며 따라서 객체화가 불가능하다. 인터페이스에 선언된 상수와 추상 메소드는 `public static final`과  `public abstract`를 생략해도 되는데 이유는 컴파일 시에 자동으로 생성해주기 때문이다. 

선언 시 `interface` 키워드를 사용한다.

```java
interface 인터페이스이름 {
    public static final 상수이름 = 값;
    public abstract void 메서드이름();
}
```
***

### ❓ 디폴트 메소드(default method)
자바8 부터 인터페이스에 디폴트 메소드를 지원한다. 디폴트 메소드의 목적은 기존 인터페이스 기능을 확장하며, 구현체에 공통적으로 들어갈 기능을 디폴트 메소드 내부에 작성함으로써 반복되는 코드의 작성을 줄여 준다. 

`default` 키워드를 반드시 붙여주어야 한다.
```java
interface Example {
  public abstract void ex1();

  //Default Method : 실행 내용까지 있음
  public default void setEx1(int ex) {
    if(ex == 1)
      System.out.println("1번 예제");
    else
      System.out.println("예제 없음");
  }
}
```
:point_right: 나중에 setEx1()의 기능이 추가되었을 때 구현체에서 고칠 필요가 없으며 인터페이스의 디폴트 메소드 내부 코드만 수정하면 된다.
***
## ✔️ 추상클래스와 인터페이스의 차이점
추상클래스와 인터페이스의 공통점은 추상메소드를 사용할 수 있다는 것이다. 그리고 인스턴스화 될 수 없다. 그럼 왜 굳이 2가지로 나누어서 사용하는 것일까?

추상클래스가 인터페이스의 역할을 다 할 수 있는데 왜 굳이 인터페이스가 있는 걸까?

가장 큰 차이점은 **사용용도**이다.

### 1. **사용의도 차이점**
```
추상클래스는 IS -A "~이다."
인터페이스는 HAS -A "~을 할 수 있는"
```
자바의 특성상 한개의 클래스만 상속이 가능하여 **해당 클래스의 구분을 추상 클래스 상속을 통해 해결하고, 할 수 있는 기능들을 인터페이스로 구현한다.** 

추상클래스는 `extends` 키워드 그대로 **확장, 상속**을 의미함으로써, 물려주는 개념이 된다. 그렇기에 부모-자식 관계인 계층 구조를 나타낸다. 하지만 인터페이스는 상속 개념이 아닌, **동일 동작을 위한 구현을 강제화** 한다.

### 2. **공통된 기능 사용 여부**
만약 모든 클래스가 **인터페이스를 사용해서 기본 클을 구성한다면 공통으로 필요한 기능들도 모든 클래스에서 오바리이딩하여 재정의 해야하는 번거로움이 있다.** 이렇게 공통된 기능이 필요하다면 추상클래스를 이용해서 일반 메소드를 작성하여 자식 클래스에서 사용할 수 있도록 하면 된다.

그러면 그냥 추상클래스만 사용하면 된다 생각할 수도 있지만 자바는 하나의 클래스만 상속 가능하기에 만약 각각 다른 추상 클래스를 상속하는데 공통된 기능이 필요하다면 인터페이스로 작성해서 구현하는 것이 편하다.

```
인터페이스는 [be able to] : ~할 수 있는
추상 클래스는 [is a kind of] : ~의 한 종류
```
***

## ✔️ 추상클래스 인터페이스 예제
![image](https://user-images.githubusercontent.com/78305431/129481605-2b6c9763-5942-4d18-ae3e-75686201204b.png)
위와 같은 관계를 갖는 예제이다. 말과 캥거루는 동물을 상속하고 말은 탈 수 있다는 기능을 인터페이스로 구현했다.

```java
/**
* 동물 추상 클래스
*/
@Getter @Setter
public abstract class Animal {
	  private String name;
	  private String leg;

	  /* Abstract method */
	  abstract void run();
}

/**
* 탈 수 있는(Ridable) 인터페이스
*/
public interface Ridable {

	  /**
	  * Abstract method 
	  * @riderName
	  */
	void youCanRide(String riderName);
}

/**
* 추상클래스를 상속 받고 인터페이스를 구현한 Horse 클래스
*/
public class Horse extends Animal implements Ridable {

	@Override
	public void run() {
		System.out.println(this.getName()+"은(는) 네 발로 뛴다.");
	}
  
	@Override
	public void ridable(String riderName) {
		System.out.println(this.getName()+"은(는) "+riderName+"을(를) 태울 수 있다.");
	}
  
}

/**
* 추상클래스를 상속 받은 Kangaroo 클래스
*/
public class Kangaroo extends Animal {

	@Override
	public void run() {
		System.out.println(this.getName()+"은(는) 네 발로 뛴다.");
	}
  
}

public class MainClass {
	public static void main(String[] args) {
		Horse horse = new Horse();
    		Kangaroo kangol = new Kangaroo();
    
		/* 상속받은 말의 속성 */
		horse.setName("얼룩말");
		horse.setLeg("다리 4개");
    
   		 /* 상속받은 캥거루의 속성 */
		kangol.setName("캥거루");
		kangol.setLeg("다리 4개");
    
		/* 말 구현체의 메서드 호출 */
   		horse.run();
		horse.ridable("BAEKJH");
    
	        /*  구현체의 메서드 호출 */
		kangol.run();
	}
}
```

### Animal 추상 클래스
```
말 is a kind of 동물
캥거루 is a kind of 동물
```
동물의 다리 개수 `leg`와 이름`name`을 입력받고 이를 통해 어떻게 움직이는지`run()`에 관한 부분은 공통적인 기능이지만 다른 기능으로 구현해야 하기 때문에 추상 클래스를 통해 구현했다. 

### Ridable 인터페이스
```
말 is able to 타다
```
말과 캥거루는 동물이기 때문에 Animal 클래스를 상속했다. 말은 캥거루와 다르게 사람이 탈 수 있는 기능을 가지고 있다. 이처럼 같은 동물 클래스라도 탈 수 있을 수도 있고 없을 수도 있기 때문에 인터페이스로 따로 선언해줘서 클래스에 구현시켜주면 **가독성도 좋고 유지보수하는 측면에서도 뛰어나다!**


### ❓ 인터페이스 이름 규칙
인터페이스 네이밍 규칙이 보통 `xxxable` 형식으로 짓는다. 구현체 네이밍은 `xxxImpl`과 같이 클래스 이름을 짓는다.

***
## ✔️ 정리
- 추상 클래스 사용 
  + 상속 관계를 타고 올라갔을때 같은 조상 클래스를 상속하는데 기능까지 완벽히 똑같은 기능이 필요한 경우
- 인터페이스 사용
  + 상속 관계를 타고 올라갔을때 다른 조상클래스를 상속하는데 같은 기능이 필요할 경우 인터페이스 사용

***

참고 - https://mygumi.tistory.com/257

https://myjamong.tistory.com/150


https://webdevtechblog.com/%EC%9E%90%EB%B0%94-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%99%80-%EC%B6%94%EC%83%81%ED%81%B4%EB%9E%98%EC%8A%A4-6eecbe5d6350