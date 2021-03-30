---
title: "추상클래스 VS 인터페이스"
date: 2021-03-25 00:00:28 -0400
draft: false
description: "[JAVA]추상클래스 VS 인터페이스"
categories: [JAVA]
toc : true
toc_sticky : true
toc_label : 목차
---

## 추상클래스란?(IS-A)
- 일반 클래스와 별 다를 것이 없지만 추상메소드가 한개라도 있어야함.
- 상속을 통해 자손 클래스에서 완성하도록 유도하는 클래스.
- 미완성 설계도이며 상속을 위한 클래스이기 때문에 객체를 생성할 수 없음.
- 공통된 기능이 필요하다면 추상클래스에서 기본 메소드를 작성하여 자식 클래스에서 사용가능할 수 있도록 함.
- 멤버변수, 기본 메소드를 가진다.
- 다중상속 불가능
``` java

public abstract class Creature{
	private int x;
	private int y;
	private int age;

	public void age(){
		age++;
	}

	public abstract void attack();  //추상메소드는 구현부 {}가 없음
	...
}		

```
**extends로 상속받음**
``` java

public class Dog extends Creature{
	public void attack(){	//오버라이딩
		...
	}
}		

```
## 인터페이스란?(HAS-A)
- 기본 설계도이며 추상메소드만을 갖는다. 일반 변수, 일반 메소드 가질 수 없음.
- **다중상속 가능**
- 인스턴스화 할 수 없음.
- 추상클래스를 상속받는 경우 추상 메소드만 재정의 하는데 이를 통해 확장, 상속을 의미한다는 것을 알 수 잇음. 
- 인터페이스는 모든 메소드가 추상 메소드이기 때문에 모든 메소드를 재정의 함. 따라서 인터페이스는 상속개념보다는 **동일한 동작을 위한 구현을 강제화** 한다. 

```java
public interface Vehicle{
	abstract void run();	//추상메소드는 구현부 {}가 없음
	abstract void move();
}

```
****
```java
public class Car implements Vehicle{
	public Car(){}

	public void run(){	//오버라이딩
		...
	}
	public void move(){	//오버라이딩
		...	
	}
}

```


