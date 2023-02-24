---
title: 5. Inheritance & Package
layout: default
#nav_order: 2
parent: Java
#permalink: /1.Java/
---

# 4_inheritance_package

## 상속(inheritance)

### `class 자식클래스 extends 부모클래스`

- 클래스 간 계층적 관계를 구성
- 다단계 상속: 3개 이상의 클래스간 상속도 가능
    - 계층적인 관계를 정의할 때 유용
- 슈퍼클래스(부모클래스) & 서브클래스(자식클래스)
- 자식 클래스는 부모클래스의 모든 멤버 사용가능

{. :highlight}
💡 한 클래스가 여러 부모클래스 상속불가
클래스가 그 자체를 상속 불가


- 부모클래스의 `private` 변수는 접근 불가
- 기존 클래스를 상속 후 필요한 것만 추가가능

`부모클래스 참조자 = new 자식클래스();`

- 자식 클래스 오브젝트 참조가능
- 자식 클래스 멤버는 접근 불가→부모 클래스 참조자는 모르는 멤버이기 때문
- 서브 클래스 생성자가 슈퍼 클래스 멤버에 직접 접근→문제점
    
    ```cpp
    class ColorRec extends Rectangle {
    	double color;
    	ColorRec(double w, double h, double c) {
    		**this.width = w;
    		this.height = h;**
    		this.color = c
    	}
    }
    ```
    

### `super(...);`

- 슈퍼 클래스 생성자 호출
    
    ```cpp
    class ColorRec extends Rectangle {
    	ColorRec(double w, double h, double c) {
    		**super(w, h);**
    		this.color = c;
    	}
    }
    ```
    
- 슈퍼 클래스의 멤버를 참조할 떄 사용(this와 유사)
    
    ```cpp
    class A {
    	int i;
    }
    class B extends A {
    	B(int a, int b) {
    		**super.i = a;//A의 i를 참조**
    		i = b;
    	}
    }
    ```
    

### 생성자 실행 순서

- 생성자는 슈퍼 클래스부터 차례대로 실행
- `super()` 생성자를 호출하지 않는 경우
→ 각 슈퍼클래스 별로 기본 생성자가 호출

```cpp
class A {
	A() {
		System.out.println(“A”);
	}
}
class B extends A {
	B() {
		System.out.println(“B”);
	} 
}
class C extends B {
	C() {
		System.out.println(“C”);
	}
}

class CallingCons {
	public static void main(String[] args) {
		C c = new C();
	}
}
//A B C
```

---

### 메서드 오버라이딩(overriding)

- 서브 클래스 메서드가 슈퍼 클래스 메서드와 동일 이름, 타입일 때 메서드를 오버라이드
    - 오버로딩과는 다름
- 오버라이딩 장점
    - 런타임 다형성의 실현: 재컴파일 없이 실행 메서드를 동적으로 결정
    - One interface, multiple methods : 슈퍼클래스와의 호환성 유지 가능
    - 동일 이름으로 계층별 다른 구현 실현: 서브 클래스에서 구현 추가 가능
- 호출 시 오버라이드 된 메서드 실행

```cpp
class A {
	int i, j;
	//..
	void show() {
		System.out.println(“i: “ + i + “j: “ + j);
	}
}
class B extends A {
	int k;
	//..
	**void show() {//A의 show()를 오버라이드**
		System.out.println(“k: “ + k);
	}
}
//..
B subOb = new B(1, 2, 3);
**subOb.show();
// K: 3**
```

- 오버라이드된 슈퍼클래스 메서드 참조시 → `super` 키워드 사용
    
    ```cpp
    class B extends A {
    	int k;
    	//..
    	void show() {
    		**super.show();**
    		System.out.println(“k: “ + k);
    	}
    }
    ```
    
- 오버로딩 vs. 오버라이딩
    - 오버라이딩: 같은 이름과 타입을 사용할 때만
    - 그 외는 오버로딩
        
        (메서드 매개변수가 다를때)
        
    
    ```cpp
    class A {
    	int i, j;
    	//..
    	void show() {
    		System.out.println(“i: “ + i + “j: “ + j);
    	}
    }
    class B extends A {
    	int k;
    	//..
    	**void show(String msg)** {//메서드 타입이 다름->오버로딩
    		System.out.println(“k: “ + k);
    	}
    }
    ```
    

---

### 동적 메서드 디스패치(dynamic method dispatch)

- 호출할 메서드를 런타임에 선택하는 방법
- 슈퍼 클래스 변수는 서브 클래스 오브젝트 참조 가능
- 클래스 변수 타입에 따라 메서드를 결정

```cpp
class A {
	void callme() {
		System.out.println(“Inside A’s callme”);
	}
}
class B extends A {
	void callme() {
		System.out.println(“Inside B’s callme”);
	}
}
class C extends A {
	void callme() {
		System.out.println(“Inside C’s callme”);
	}
}
//…
A a = new A();
B b = new B();
C c = new C();

A r;

r = a;
r.callme();//A의 callme()호출

r = b;
r.callme();//B의 callme()호출

r = c;
r.callme();//C의 callme()호출
```

---

### 추상클래스(abstract class)

`abstract`

- 구현 없이 클래스의 구조만 선언할 때
    - 서브 클래스에서 상속 후 구현
- 해당 단계에서 구현할 내용이 딱히 없을 때 유용
- `abstract` 키워드: 추상 클래스 및 메서드 정의 가능

```cpp
abstract class A {
	abstract void callme();
	void callmetoo() {//추상 클래스 내부에 일반 메서드도 정의 가능
		System.out.println(“concrete method”);
	}
}
class B extends A {
	void callme() {//추상 클래스 A를 상속하여 구
		System.out.println(“implementation”);
	}
}

//A a = new A();추상클래스는 인스턴스화 불가

//But, 추상 클래스 변수로 서브 클래스 오브젝트를 참조 가능
B b = new B();
b.callme();
A a = b;
```

---

### `final` 메서드

- 서브 클래스가 베서드 구현 변경을 못하도록 할 때
- 성능 상의 장점
    - 런타임에 오버라이딩 검사 필요 X
    - 컴파일 타임에 사용 메서드 바로 결정 가능
    
    ```cpp
    class A {
    	final void meth() {
    		System.out.println(“final method”);
    	}
    }
    class B extends A {
    	void meth() {//final로 지정된 메서드는 오버라이딩 불가
    		System.out.println(“illegal”);
    	}
    }
    ```
    

### `final` 클래스

- `final` 로 지정된 클래스는 상속 불가 → 컴사일 에러

---

### object클래스

- 모든 클래스가 상속하는 java의 기본 클래스
- 오브젝트를 다룰 때 사용하는 유용한 메서드 제공
- 몇몇을 제외하고 오버라이딩 가능

| 메서드 | 목적 |
| --- | --- |
| `Object clone()` | 오브젝트 복제 |
| `boolean equals(Object object)` | 오브젝트가 같은지 검사 |
| `void() finalize` | 오브젝트가 소멸 전 호출(JDK9에서 삭제) |
| `Class<?> getClass()` | 오브젝트릐 클래스 리턴 |
| `int hashCode()` | 오브젝트의 해쉬값 계산 |
| `void notify()` | 오브젝트를 사용하는 쓰레드의 실행 재개 |
| `void notifyAll()` | 오브젝트를 사용하는 모든 쓰레드의 실행 재개 |
| `String toString()` | 오브젝트를 설명하는 문자열 반환 |
| `void wait()` `void wait(long milliseconds)` `void wait(long milliseconds, int nanoseconds)` | 다른 쓰레드의 실행이 끝날 때까지 대기 |
           

---

## 패키지

- 네임스페이스(namespace)를 구성하는 요소
- 네임스페이스: 클래스가 유일 이름을 가지는 단위

### `package 패키지_이름`

- Java소스파일 최상단에 정의
- 대소문자 구분
- 패키지 정의 생략 시 Java의 기본 패키지 사용

### 패키지와 파일 시스템

- Java는 파일 시스템을 이용해 패키지 관리
- 해당 패키지 이름을 가진 디렉토리가 존재해야함
mypackage선언 시 소스파일이 mypackage디렉토리에 있어야 함

### 계층적 패키지 정의

`package 패키지1.[.패키지2[.패키지3]];`

- `.` → 계층적으로 분리 가능
    - 각 분리된 패키지별 디렉토리가 존재햐야 함
- `package a.b.c;`
    - 소스파일이 a/b/c/경로에 있어야함

### 패키지 검색 방법 가지

1. 현재 디렉토리부터 하위 디렉토리 검색
2. CLASSPATH 환경 변수 참조
3. 컴파일 및 실행 시 `-classpath` 옵션으로 지정
    - 패키지보다 상의 디렉토리 경로를 지정해야함
    - mypack패키지를 찾는 경우 <br>
    ~~C:\MyPrograms\Java\mypack~~ <br>
    C:\MyPrograms\Java
- AccountBalance.java소스 파일에 mypack이라는 패키지 선언
`package mypack;`
    - mypack디렉토리를 만든 후 AccountBalance.class파일을 이동
    - `java mypack.AccountBalance` 해당클래스 파일 실행 가능
    - mypack 디렉토리보다 상위에 있어야 함

### 패키지와 접근 제어

- 패키지는 접근제어의 또 하나의 차원
- 상속관계와 함께 4가지 졍우
    1. 상속 관계, 같은 패키지
    2. 상속 관계X, 같은 패키지
    3. 상속 관계, 다른 패키지
    4. 상속 관계X, 다른 패키지
    
    |  | private | 접근제어자 없을 때 | protected | public |
    | --- | --- | --- | --- | --- |
    | 상속 관계, 같은 패키지 | X | O | O | O |
    | 상속 관계X, 같은 패키지 | X | O | O | O |
    | 상속 관계, 다른 패키지 | X | X | O | O |
    | 상속 관계X, 다른 패키지 | X | X | X | O |
    | 같은 클래스 | O | O | O | O |
    - 접근 제어자가 없으면(default멤버일때) 같은 패키지 내에선 접근가능
    - protected로 지정 시 다른 패키지여도 상속 관계면 접근 가능
    - private멤버는 오직 같은 클래스 내부에서만 접근 가능
- 2개의 패키지와 5개의 클래스
    
    ![Untitled](https://user-images.githubusercontent.com/98319061/221088839-242d706e-bdab-41bb-87da-23666d88b319.png)

    

```cpp
//Protection.java
package p1;
public class Protection {
	int n = 1;
	private int n_pri = 2;
	protected int n_pro = 3;
	public int n_pub = 4;
	public Protection() {
		System.out.println("base constructor");
		System.out.println("n = " + n);
		System.out.println("n_pri = " + n_pri);
		System.out.println("n_pro = " + n_pro);
		System.out.println("n_pub = " + n_pub);
	}
}
```

```cpp
//Derived.java
package p1;
class Derived extends Protection {
		Derived() {
			System.out.println("derived constructor");
			System.out.println("n = " + n);

// private 변수 접근 불가
// System.out.println("n_pri = " + n_pri);

		System.out.println("n_pro = " + n_pro);
		System.out.println("n_pub = " + n_pub);
	}
}
```

```cpp
//SamePackage.java
package p1
class SamePackage {
	SamePackage() {
		Protection p = new Protection();
		System.out.println("same package constructor");
		System.out.println("n = " + p.n);

// private 변수 접근 불가
// System.out.println("n_pri = " + p.n_pri);

		System.out.println("n_pro = " + p.n_pro);
		System.out.println("n_pub = " + p.n_pub);
	}
}
```

```cpp
//Protection2.java
package p2;
class Protection2 extends p1.Protection {
	Protection2() {
		System.out.println("derived other package constructor");

// 다른 패키지의 default 변수 접근 불가
// System.out.println("n = " + n);

// private 변수 접근 불가
// System.out.println("n_pri = " + n_pri);

		System.out.println("n_pro = " + n_pro);
		System.out.println("n_pub = " + n_pub);
	}
}
```

```cpp
//OtherPackage.java
package p2
class OtherPackage {
	OtherPackage() {
		p1.Protection p = new **p1.Protection();**
		System.out.println("other package");

// 다른 패키지 default 변수 접근 불가
// System.out.println("n = " + p.n);

// private 변수 접근 불가
// System.out.println("n_pri = " + p.n_pri);

// 상속 관계가 아니면 protected 변수 접근 불가
// System.out.println("n_pro = " + p.n_pro);

		System.out.println("n_pub = " + p.n_pub);
	}
}
```

---

### import문

- 패키지로 클래스를 묶으면 라이브러리로 사용 편리
    - But…매번 패키지 이름을 명시해야함(`p1.Protection`)

`import 패키지1[.패키지2].(클래스_이름|*);`

- 특정 클래스나 패키지를 import가능
- `import java.util.Date` : java.util패키지의 Date클래스를 import
- `import java.io.*;` : java.io 패키지의 모든 클래스를 import

```cpp
//Balance.java
package mypack;
public class Balance {
	String name;
	double bal;
	public Balance(String n, double b) {
		name = n;
		bal = b;
}
	public void show() {
		if(bal<0) 
		System.out.print("-->> ");
		System.out.println(name + ": $" + bal);
	}
}
```

```cpp
//TestBalance.java
import mypack.*;
class TestBalance {
	public static void main(String[] args) {
		Balance test = new Balance("J. J. Jaspers", 99.88);
//Balance클래스와 public메서드 show()에 패키지 이름 없이 접근가능
		test.show(); 
	}
}
```