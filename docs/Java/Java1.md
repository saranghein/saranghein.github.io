---
title: 1. Java
layout: default
#nav_order: 2
parent: Java
#permalink: /1.Java/
---

# 1. Java

목차
[Java의 역사 및 특징](#java의-역사-및-특징)
[객체지향프로그래밍](#객체지향프로그래밍)
[Java 기본문법](#java-기본문법)

# Java의 역사 및 특징

> Java
> 

객체지향, 클래스 기반, 플랫폼 독립적 프로그래밍
Write Once Run Anywhere(WORA)
C → C++ → Java

---

> C
> 

1970년대 Dennis Ritchie에 의해 개발
프로그래머 친화적인 structed programming(if/then/else, while, for)→기존 BASIC, COBOL, FORTRAN등의 복잡성 해결
BUT 여전히 프로그램 크기가 커질 때 복잡해지는 문제발생

> C++
> 

1979년 Bjarne Stroustrup에 의해 개발
C with Classes→C++
기존언어 + 객체지향프로그래밍 특성
1980s~1990초 객체지향프로그래밍 언어로 널리 사용

<aside>
💡 C, C++는 코드를 특정 CPU타겟에 맞춰 컴파일필요
→모든 CPU에 대해 컴파일러를 만들면 개발자에게 많은 비용과 시간을 요구

</aside>

---

## Java의 등장

- 1991년 James Gosling을 필두로 한 Sun Microsystems*의 연구원들이 개발
*2009년 Oracle이 인수
- Oak → java(1995년)
- 플랫폼 독립적(paltform independent)언어로 개발(본래 가전제품 컨트롤러에서 실행되는)
: 당시에는 가전제품 하드웨어 칩의 성능 이슈로 시기상조
- World Wide Web의 등장으로 중요성 부각
: Web에는 다양한 운영체제와 하드웨어가 공존
  어느 시스템에서도 실행가능한 프로그램의 필요성 대두
- Web의 발전과 함께 급속도로 퍼짐

## Java의 특징

- 이식성(portability) & 보안성(security)
- 인터넷의 발전→다양한 네트워크 시스템
”네트워크 시스템은 어느 플랫폼에서도 동작하며(이식성), 악성코드의 실행으로부터 안전해야함(보안성)”
- java의 동작원리는 이식성, 보안성을 만족시킴

## Java의 동작원리

<aside>
💡 C, C++코드가 기계어로 컴파일 되는 것과 대비

</aside>

- java코드는 컴파일 시 중간언어인 **바이트코드(bytecode)**로 변환
- **자바 가상 머신(Java Virtual Machine, JVM)**에서 실행
    - JVM은 자바 런타임 환경(Java Runtime Environment, JRE)의 일부

![Untitled](https://user-images.githubusercontent.com/98319061/218664314-ce49660b-6b87-44af-b7a6-547cf5bbd39c.png)

- JRE만 있으면 어느 프로그램이든 실행가능(이식성)
- JVM내에서 실행돼 안전(보안성)→샌드박싱(sandboxing)

![Untitled 1](https://user-images.githubusercontent.com/98319061/218664303-fca20713-0e7a-4727-9f4f-c1cd219487c2.png)

- JBM은 바이트코드 해석 후 실행이 요구됨→낮은 성능 이슈
→ JIT(Just-in-time)컴파일러가 JVM에 포함됨→런타임에 바이트코드를 기계어로 해석하여 실행(유튜브에서 미리 영상로딩하는 것처럼)
- JDK(Java Delvelopment Kit)를 이용해 개발
    - OpenJDK
        
        Sun Microsystems 에서 2007년 공개한 오픈소스 JDK
        
        GPL(General Public License)적용
        
    - Oracle JDK
        
        Oracle에서 제공하는 JDK
        
        NFTC(No-Fee Terms and Conditions)라이센스 적용
        

![Untitled 2](https://user-images.githubusercontent.com/98319061/218664308-b7075e8a-cf77-4096-9862-301ef23152cb.png)

## Java applet

- java의 대표적 웹 애플리케이션(JRX를 지원하는 브라우저면 프로그램 실행 가능)
- 브라우저들에게 플러그인 지원을 강제(공인인증서 설치)
→2017년 Java9부터 퇴출됨

## Java servlet

| applet | servlet |
| --- | --- |
| 클라이언트 프로그램 | 서버 프로그램 |
- 데이터베이스 등과 연동하여 클라이언트 요청처리
- JRE를 지원하는 모든 서버에서 실행가능

## Java 릴리즈 히스토리

- Java 1.4 까지는 J2SE(Java 2 Platform Standard Edition)로 명칭
- Java 1.5부터 대규모 업데이트(제네릭, 어노테이션, 오토박싱, 열거형, for-each 등)→ Java 5로 개명
- Java10부터 6개월 단위로 업데이트

![Java 릴리즈 히스토리](https://user-images.githubusercontent.com/98319061/218664310-3b1d0218-3801-4e98-b220-c9371de1acb8.png)

Java 릴리즈 히스토리

## Java Buzzwords

> 간단함(simple)
> 

프로그래머 친화적

> 견고함(robust)
> 

메모리 오류로부터 안전

> 멀티쓰레드 지원(multithreaded)
> 

병렬처리 구현이 쉬움

> 고성능(high-performance)
> 

JIT컴파일러로 성능 최적화

> 분산(distributed)
> 

분산 네트워크 환경에 친화적

> 객체지향적(object-oriented)
> 

C++보다 더 객체지향적

---

# 객체지향프로그래밍

## 프로그래밍 패러다임

- program=code+data
- process-oriented(절차지향)
    - **코드**를 중심으로 하는 프로그래밍 기법
    - 프로그램의 크기가 커질수록 복잡해지고 확장이 어려움
- object-oriented(객체지향)
    - **데이터**를 중심으로 하는 프로그래밍 기법
    - 절차지향에 비해 더 직관적

## Abstraction(추상화)

- 모든것을 object화하여 복잡성 해결
- Java는 3가지 원리에 기반해 달성

## 원리

### encapsulation(캡슐화)

- 관련 데이터와 코드를 하나로 묶어 외부로부터 은닉
    - 외부에서 임의로 접근하지 못하도록 보호
- interface를 통해서만 제어가능
    - ex) 리모콘 조작을 위해 사용자는 버튼 이용
- 구현이 달라도 사용자에게 동일 인터페이스 제공
- Java는 class단위로 캡슐화
    - 오브젝트의 데이터와 코드를 정의한 설계도
    - 코드를 method단위로 묶고 접근자를 설정하여 은닉

### inheritance(상속)

- 한 오브젝트가 다른 오브젝트의 특징을 물려받는 것
- 상속으로 계층적구조정의
- 부모-자식 클래스 관계 or 상위-하위 클래스
    - 자식 클래스는 부모 클래스의 특징 물려받음

### polymorphism(다형성)

- 동일한 인터페이스가 서로 다른 클래스에서 동작하도록 적용
- 행위는 동일 but 입력 데이터에 따라 action달라짐
- 정수형, 실수형, 문자형 stack 구현할 때
- C의 경우
    - 각 타입 별로 구현 후 개별 인터페이스 정의 필요
- Java의 경우
    - 구현 후 공통적인 인터페이스를 통해 사용
    - 데이터에 따라 적용할 구현체를 JIT컴파일러가 알아서 선택

---

# Java 기본문법

## EX1

```java
/* 
	This is a simple Java progrma.
	Call this file "Example.java".
*/
//Your program begins with a call to main().
	
public static void main(String [] args) {
	System.out.println("This is a simple Java program.");
}
```

### 주석

### 주석(comment)

- 프로그램에 대한 설명 기록
- 컴파일 대상에서 제외됨

| 다수라인주석 | /* … */ |
| --- | --- |
| 단일라인주석 | // |

### `public static void main(String [] args) {`

### `class`

`class *className* { … }` 

- 자바 소스파일은 하나 이상의 클래스를 포한
- 모든 코드는 클래스 내부에서 정의

### `main()`

- Java 프로그램이 시작되는 곳

### `public`

- 접근제어자(access modifier)를 의미, 클래스 멤버의 접근성 결정
    
    <aside>
    💡 className도 인자
    
    </aside>
    

| public | 외부의 접근 허용 |
| --- | --- |
| private | 외부의 접근 제한 |

### `String[] args`

- main()메서의 인자(argument)
- String class의 배열 array이며 커맨드라인의 인자를 받음

### `System.out.println(…);`

### `println()`

- Java 문자열의 출력 표준 메서드
- 문자열 출력 후 행 변경(newline)

### `System.out`

- System은 JVM이 실행되는 시스템을 의미하는 built-in 클래스
- out은 출력 스트림

### `;`

- 실행문(statement)은 세미콜론으로 끝남

---

## EX2

```java
/*
Here is another short example.
Call this file "Example2.java".
*/
class Example2 {
	public static void main(String[] args) {
		int num; // this declares a variable called num
		num = 100; // this assigns num the value 100
		System.out.println("This is num: " + num);
		num = num * 2;
		System.out.print("The value of num * 2 is ");
		System.out.println(num);
	}
}
```

### 변수(variable)

`type *variableName*`

- 프로그램 실행 중 임시로 값을 저장하는 역할

### `System.out.println("This is num: " + num);`

- 문자열에 num변수 값을 추가( + 기호)

### `print()`

- println과 다르게 행변경을 하지 않음

---

## EX3

```java
class IfSample {
	public static void main(String[] args) {
		int x, y;
		x = 10;
		y = 20;
		if(x < y) System.out.println("x is less than y");
		x = x * 2;
		if(x == y) System.out.println("x now equal to y");
		x = x * 2;
		if(x > y) System.out.println("x now greater than y");
		// this won't display anything
		if(x == y) System.out.println("you won't see this");
	}
}
```

### If문

`if(조건문)실행문;`

- 조건문 만족→실행문 트리거

---

## EX4

```java
class ForTest {
	public static void main(String[] args) {
		int x;
		for(x = 0; x < 10; x = x + 1)
		System.out.println("This is x: " + x);
	}
}
```

### for문

`for(초기식;조건식;증감식)`

- 초기식(initialization)
    
    제어문 변수의 값을 초기화
    
    초기 C에서는 정의와 동시에 초기화 안됐지만 java는 첨부터 됨
    
- 조건식(condition)
    
    매 루프마다 조건식 평가
    
    True일 경우 실행문 실행
    
- 증감식(iteration)
    
    제어문 변수를 어떻게 변경할 것인지 명시
    
    대개 증감연산자(increment/decrement operator)를 이용
    

---

## EX5

```java
class BlockTest {
	public static void main(String[] args) {
		int x, y;
		y = 20;
		// the target of this loop is a block
		for(x = 0; x<10; x++) {
			System.out.println("This is x: " + x);
			System.out.println("This is y: " + y);
			y = y - 2;
		}
	}
}
```

### 코드블록(code blocks)

- C/C++처럼 코드블록 허용
- for/if/while문 등에서 사용

---

## 공백문자(whitespace)

- Java는 자유형식언어(free-form language)
    - Python 등과 같이 들여쓰기(indent)불필요
    (한 줄로 써도 됨 → ; 로 구분)
- 키워드와 식별자 간에 임의의 공백문자*만 필요
    
    *스페이스, 탭, 개행문자 등 (`Class Example { … }`)
    

## 식별자(identifier)

- 클래스, 변수, 메서드의 이름
- 식별자 규칙
    - 문자, 언더바(_), $로 시작
    
    <aside>
    💡 언더바보다는 문자를 선호
    
    </aside>
    
    - 대소문자 구분
    - +, - 등 연산자 포함 금지
    - Java키워드 사용금지
    - 길이 무제한
- AvgTemp, count, a4, this_ok
- ~~2count, high-temp, Not/ok~~

---

## 키워드(keyword)

- java는 67개의 키워드를 정의

![Untitled 4](https://user-images.githubusercontent.com/98319061/218664312-02457e53-a1db-4a22-9bc8-929a7918554a.png)

---

## Java클래스 라이브러리

- 대부분의 Java프로그램은 여러 표준 클래스 사용
- EX의 `println()`, `print()` 은 빌트인 메서드
    - `System.out`을 통해 사용가능
    - System은 Java프로그램에 자동으로 포함되는 표준 클래스