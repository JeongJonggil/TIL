# 객체지향 프로그래밍

### 1. 개요

- 객체지향 프로그래밍(OOP, Object Oriented Programming)

  - 객체 : 사물과 같이 유형적인 것과 개념이나 논리와 같은 무형적인 것들

  - 지향 : 작정하거나 지정한 방향으로 나아감

  - 객체 모델링 : 현실세계의 객체를 SW 객체로 설계하는 것

- 클래스(Class)
  - 객체를 만드는 설계도(Blueprint)
  - **상태와 행동을 묶어서 만든 사용자정의 자료형**

- 인스턴스(Instance)
  - 클래스를 통해 생성된 객체

### 2. 특징

- A PIE
  - Abstraction(추상화)
  - Polymorphism(다형성)
  - Inheritance(상속)
  - Encapsulation(캡슐화)
- 장점
  - 모듈화된 프로그래밍
  - 재사용성이 높다

###  3. 코드

```java
public class Person{
	String name;
	int age;
	String hobby;
	
	public void info() {
		System.out.println("나의 이름은" + name +"입니다")
		System.out.println("나이는"+age", 취미는"+ hobby +"입니다");

	}
}
```

### 4. 클래스 구성

- 속성(Attribute) - 필드
- 동작(Behavior) - 메소드
- 생성자(Constructor) - 특수한 함수
- 중첩 클래스(클래스 내부의 클래스)



### 5. 클래스 선언

- [접근제한자(public/default)] [활용제한자(final/abstract)] class 클래스명 { 

  ​	속성 정의 (필드)

  ​	기능 정의 (메소드)

  ​	생성자

  }

```java
public class Person {
	String name;
	int age;
	
	publick void eat(){
	}
	
	public Person(){
	}
}
```



### 6. 변수

- 클래스 변수
  - 클래스 영역 선언 (static 키워드)
  - 생성시기: 클래스가 메모리에 올라 갔을 때
  - 모든 인스턴스가 공유함
- 인스턴스 변수
  - 클래스 영역 선언
  - 생성시기 : 인스턴스가 생성되었을 때 (new)
  - 인스턴스 별로 생성됨
- 지역 변수
  - 클래스 영역 이외 (메서드,생성자 등)
  - 생성시기 : 선언되었을 떄

### 7. 메소드

- 리턴 타입은 메소드를 선언할 때 지정, 없다면 void (return 문 생략 가능)

- 리턴 타입을 작성했다면 반드시 해당 타입의 값을 리턴

- 리턴 타입은 하나만 적용 가능

- 메소드 오버로딩

  - 이름이 같고 매개변수가 다른 메서드를 여러 개 정의하는 것
  - 중복 코드에 대한 효율적 관리 가능
  - 파라미터의 개수 또는 순서, 타입이 달라야 할 것(파라미터 이름만 다른 것은 X)
  - 리턴 타입이 다른 것은 의미 X

  ```java
  ex)
  println(): void;
  println(boolean x): void;
  println(char x): void;
  println(char[] x): void;
  println(double x): void;
  println(float x): void;
  prinln(int x);
  ```

  
