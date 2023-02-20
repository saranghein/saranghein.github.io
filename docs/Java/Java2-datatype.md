---
title: 2. Data type
layout: default
#nav_order: 2
parent: Java
#permalink: /1.Java/
---

# 2_datatype

>## 목차
>1. [데이터 타입](#데이터-타입) <br>
>2. [변수](#변수) <br>
>3. [배열](#배열)<br>

# 데이터 타입

## Java의 언어적 특징

- Java는 Strongly Typed Language
    - 모든 변수에 type이 존재
    - 모든 변수가 사전에 정의 되어야함
    - 변수 대입, 인자 전달 시 변수 간 타입 호환 요구
- 컴파일 타임에 상기 사항을 엄격하게 검사
(동적언어와 구분됨 JavaScript, Python…)

## 기초타입Primitive Type

- 숫자, 문자, 논리 등 기초(primitive)연산에 필요
- 단일값만을 나타냄
    - 오브젝트X
    - 기초타입ㅇ르 오브젝트로 나타낼 시 성능 저하 이슈<br>
    (클래스로 나타내면 쓸데없이 무거워지기만 함)
- 기초타입값의 범위는 고정적
    - 하드웨어 아키텍처에 의존적이지 않음 <br>
    (int 타입의 크기는 항상 32 bit)
- Java는 8개의 기초타입
    
    
    | 분류 | 기초타입 | 기억공간크기 | 기본값 | 값의 범위 |
    | --- | --- | --- | --- | --- |
    | 정수 | byte | 8bit | 0 | -128~127 |
    |  | short | 16 | 0 | -32,768~32,767 |
    |  | int | 32 | 0 | -2,147,483,648~-2,147,483,647 |
    |  | long | 64 | 0L | -9,223,372,036,854,775,808 ~ -9,223,372,036,854,775,807 |
    | 실수 | float | 32 | 0.0f | 약 ±3.4x$10^{-38}$ ~ ±3.4x$10^{+38}$ |
    |  | double | 64 | 0.0d | 약 ±1.7x$10^{-308}$ ~ 약 ±1.7$10^{+308}$ |
    | 문자 | char | 16 | null | 0(’\u0000’) ~ 65,535(’\uFFF’) |
    | 논리 | boolean | 8 | false | true와 false |

### 정수타입

- Java는 총 4가지의 정수(integer)타입 지원
byte, short, int, long
- 모두 부호형(signed)타입
- C와 달리 부호가 없는 타입(unsigned)미지원

**byte**

- 8비트 크기, -128~+128의 범위
- 소켓, 파일 스트림을 다룰 때, 네트워크 시스템에서 많이 사용
- 변수는 byte키워드를 사용해 선언

**short**

- 16비트 크기, -32.768~+32,767의 범위
- 변수는 short키워드를 사용해 선언

**int**

- 32비트 크기, -2,147,483,648~-2,147,483,647의 범위
- 정수형에서 가장 많이 사용
- 변수는 int 키워드를 사용해 선언

**long**

- 64비트 크기 $-(2^{64})$~$+(2^{64}-1)$의 범위
- int타입으로는 표현할 수 없는 큰 숫자를 나타낼 때 사용
- 변수는 long키워드를 사용
<details>
<summary>EX</summary>
<div markdown="1">
    
```java
    class Light {
    	public static void main(String[] args) {
    		int lightspeed;
    		long days;
    		long seconds;
    		long distance;
    		// approximate speed of light in miles per second
    		lightspeed = 186000;
    		days = 1000; // specify number of days here
    		seconds = days * 24 * 60 * 60; // convert to seconds
    		distance = lightspeed * seconds; // compute distance
    		System.out.print("In " + days);
    		System.out.print(" days light will travel about ");
    		System.out.println(distance + " miles.");
    	}
    }
```
</div>
</details>

---

### 부동소수점 타입

- 부동소수점 타입(floating-point)타입은 실수를 나타낼 때 사용
    - Java는 IEEE-754에 따라 부동소수점 타입을 구현
- IEEE-754(0→양수/1→음수)
    - 부동소수점 비트 표현법에 대한 표준
    - EX) -188.625을 32비트 단정밀도(Single-precision)로 나타낼 때
    
    ![Untitled](https://user-images.githubusercontent.com/98319061/218668213-8b773e46-3e62-41a4-8d67-2d8f52174440.png)

    

**float**

- 32비트의 크기를 가지는 단정밀도(Single-precision)숫자
- 작거나 높은 정밀성을 요구하지 않는 실수를 나타낼 때

**double**

- 64비트의 크기의 배정밀도(Double-precision)숫자
- `sin()`, `cos()` 등 대부분 math 클래스 메서드의 리턴 타입
<details>
<summary>EX</summary>
<div markdown="1">
    
```java
    class Area {
    	public static void main(String[] args) {
    		double pi, r, a;
    		r = 10.8; // radius of circle
    		pi = 3.1416; // pi, approximately
    		a = pi * r * r; // compute area
    		System.out.println("Area of circle is " + a);
    	}
    }
```
</div>
</details>

---

### 문자 타입

- Java는 문자 인코딩으로 유니코드(Unicode)사용(C→아스키코드)
    - 문자→숫자(인코딩)
    - 유니코드는 전 세계 글자를 나타낸 문자 집합
- 문자 기초 타입은 char타입
    - 유니코드를 위해 16비트 길이 사용
    - 0~65,535범위의 정수
    - 정수형 연산에도 사용가능
<details>
<summary>EX</summary>
<div markdown="1">
    
```java
    class CharDemo {
    	public static void main(String[] args) {
    		char ch1, ch2;
    		ch1 = 88; // code for X
    		ch2 = 'Y’;
    		System.out.print("ch1 and ch2: ");
    		System.out.println(ch1 + " " + ch2);
    	}
    }
    //X Y 출력
    //88은 아스키코드면서 유니코드
```
</div>
</details>

---

### 논리 타입

- 논리 타입으로 boolean 타입 사용
    - true or false
- if 또는 for문 등의 조건식에서 사용
    - 결과에 따라 실행흐름 결정
    - 조건식의 결과도 boolean타입으로 표현됨
<details>
<summary>EX</summary>
<div markdown="1">
    
```java
    class BoolTest {
    	public static void main(String[] args) {
    		boolean b;
    		b = false;
    		System.out.println("b is " + b);
    		b = true;
    		System.out.println("b is " + b);
    		// a boolean value can control the if statement
    		**if(b)** System.out.println("This is executed.");
    		//조건식에서 비교(==)불필요
    		b = false;
    		if(b) System.out.println("This is not executed.");
    		// outcome of a relational operator is a boolean value
    		System.out.println("10 > 9 is " + **(10 > 9)**);
    		//>>> 10 > 9 is true(조건식의 결과는 boolean으로 출력됨
    	}
    }
```
</div>
</details>


---

## 정수 리터럴

![Untitled 1](https://user-images.githubusercontent.com/98319061/218668216-72acc324-a942-47c2-acc6-accd00349d48.png)


- 리터럴(literal)
소스코드에서 코정딘 값을 표현하는 방식
- 리터럴의 진법(base)은 접두어(prefix)를 이용
    
    | 진수 | 접두어 |
    | --- | --- |
    | 10진수(decimal) | 아무 접두어가 없는 숫자는 10진수로 인식됨 |
    | 2진수(binary) | 0b or 0B (0b1010)  |
    | 8진수(octal) | 0 (01, 02, 03) |
    | 16진수(hexadecimal) | 0x or 0X (0x1, 0xA, 0XF) |
- 정수 리터럴은 기본적으로 int 타입으로 인식됨
    - byte, short 변수에 할당 → 값 범위 내면 가능(`short num=(short)21;`)
    - long변수에 할당 → 모든 정수 리터럴 가능
- long타입 리터럴
    - 접미어 `l` or `L`로 명시적 표기 가능 <br>
    0x7….L
- 언더바(underbar)
    - 정수 리터럴은 언더바 포함 가능
    - 자리수가 많은 숫자의 가독성을 위해 사용
    - `int x=123_456_789;`

---

## 부동소수점 리터럴

- 표준 표기법(standard notation)
    - 일반적인 십진수 표기법
    - 2.0, 3.141592
- 과학적 표기법(scientific notation)
    - 접미어 `E` or `e` 에 지수를 10진수로 표기
    - 6.022E23, 314158E-05
- 부동소수점 리터럴은 기본적으로 double타입으로 인식
(double이 더 정확하므로)
- float리터럴은 `F` or `f` 접미어를 붙여서 표기
- double리터럴도 `D` or `d` 접미어로 명시적 표기 가능

---

## 논리 리터럴

- true, false 두가지 리터럴
- 숫자 표현으로 변환되지 않음<br>
true, false는 1, 0으로 인식하지 않음

---

## 문자 리터럴

- 작은 따옴표(`’ ’`)와 함께 나타냄
’a’, ‘z’
- 몇몇 문자는 이스케이프 문자{ `\` )를 사용해 표현
’\’’, ‘\n’
- 접두어 ‘`\u`’를 써서 유니코드를 직접입력 가능
\u0061

![Untitled 2](https://user-images.githubusercontent.com/98319061/218668221-70b99cf5-a459-4538-bb46-bb6e67a65b12.png)


---

## 문자열 리터럴

- 문자열(string)리터럴은 쌍따옴표(`” ”`)로 표기<br>
`"Hello World"`
- 같은 행(line)에 있는 문자들만 같은 문자열로 인식
- 각 문자열은 오브젝트로 인식됨
    - C와 같이 문자들의 배열(array)로 취급되지 않음
- Java에서 문자열은 기초타입이 아닌 오브젝트
    - String클래스를 이용하여 문자열 선언 가능 <br>
    `String str=”this is a test”;`

---

# 변수

`타입 식별자 [=값] [, 식별자[=값]];`

## 변수의 동적 초기화

- 변수 선언 시 연산에 의한 동적 초기화 가능
`double c= Math.sqrt(a*a+b*b);`



## 변수의 스코프와 라이프타임

### 스코프(scope)

- 변수의 유효 범위 또는 영역
- 스코프에 따라 변수의 라이프타임(lifetime)결정
- 변수의 스코프는 블록단위로 결정됨
    - 블록은 중괄호( `{  }` )로 정의
- 블록 내에서 정의된 변수는 지역변수(local variable)
    - 지역변수는 블록 외부에서 접근할 수 없음
- Java 는 어느 블록에서는 변수 선언 허용(C99문법과 유사)
- 변수는 사용전 반드시 선언
- 중첩된 스코프(nested scope)허용
    - 블록 내에 새로운 블록을 정의 가능
    - 새로운 블록에서 변수가 선언될 수 있음
        
        ```java
        class Scope {
        	public static void **main**(String[] args) {
        		int x; // known to all code within main
        		x = 10;
        		**if**(x == 10) { // start new scope
        			int y = 20; // known only to this block
        			// x and y both known here.
        			System.out.println("x and y: " + x + " " + y);
        			x = y * 2;
        		}//블록이 끝난 후 y는 유효하지 않음
        		// y = 100; // Error! y not known here
        		// x is still known here.
        		System.out.println("x is " + x);
        	}
        }
        ```
        
- 변수 선언과 초기화가 포함된 코드 블록 실행 시
해당 코드 블록이 실행 될 때마다 초기화가 진행됨
    
    ```java
    for(int x = 0; x < 3; x++) {
    	**int y = -1;**//y는 매 루프마다 -1로 초기화 됨
    	System.out.println("y is: " + y);
    	// this always prints -1
    	y = 100;
    	System.out.println("y is now: " + y);
    }
    ```
    
- 동일한 변수명을 중첩된 블록에서 선언 불가
    ```java
    public static void main(String[] args) {
	    **int bar = 1;**
	    { // creates a new scope
	    **int bar = 2;**
	    // Compile time error -- bar already defined!
	    //bar변수가 재선언 되어 컴파일 에러 발생
	    }
    }
    ```

---

## 타입 변환(Type Conversion)

- 변수를 다른 타입으로 변환하는 것
- 다음 두 조건을 만족 시 자동 타입 변환 수행
    1. 두 타입이 호환될 때
    2. 대상 타입이 현재 타입 보다 클 때
        
        byte → int
        
        ~~char → boolean~~
        
- 확대 변환(widening conversion)이라고도 함

## 타입 캐스팅(Type Casting)

- 큰 타입에서 작은 타입으로 변환할 때
    - 자동 타입 변환 적용 불가
        
        int → byte
        
- 축소 변환(narrowing conversion)이라고도 함
- `(목표 타입)값` 형태로 캐스팅 수행
    
    `int a;`
    `byte b=(byte)a;`
    

## 버림(Truncation)

- 부동 소수점 값이 정수형 타입 변수에 할당 될 때
- 소수점 이하 자리수가 버려지게 됨

```cpp
byte b;
int i = 257;
double d = 323.142;
//하위 1바이트만 취함
b = (byte) i;//b:1
b = (byte) d;//b:67
//소수점 이하 .142버림
i = (int) d;//i:323
```

## 타입 승격(Type Promotion)

- 연산식(expression)에서의 자동 타입 변환
    - 중간 값이 타입 값 범위를 벗어 날 때
- Java는 자동으로 중간값을 int 타입으로 승격

```cpp
byte a = 40;
byte b = 50;
int c = a * b;//a*b를 int타입으로 승격
~~byte d = a * b;//2000으로 byte타입 범위를 벗어남
b=b*2;//b*2가 int타입으로 승격되었으므로 error~~
b=(byte)(b*2);//수정
```

## 타입 승격 규칙

- 연산식의 피연산자(operand)가
    - byte, short, char→int
    - 하나라도 long→long
    - 하나라도 float→float
    - 하나라도double→double

## 타입 추론(Type Inference)

- 값을 통해 변수의 타입을 추론
    - Java10에 추가된 기능
    - 타입의 명시적 선언이 필요없어 코드의 간소화 가능
    - `var` 사용
- `var avg=10.0;` → `double avg=10.0;
 var myArray=new int[10];` →`int[] myArray=new int[10];`
- 식별자(변수)로도 사용가능
    - 클래스, 인터페이스 명으로는 사용불가
- 배열 변수에 대괄호 표기 불필요
`~~var[] myArray = new int[10];~~`
`~~var myArray[] = new int[10];~~`
- 사용시 값 초기화 필수
`~~var counter;~~`
- 지역 변수로만 사용가능
    - 오브젝트, 함수인자, 리턴 값으로 사용 불가
- 배열 초기화로 사용 불가
`~~var myArray={1,2,3};~~
 var myArray=new int[10];`

# 배열

> 배열
> 

배열(array)은 여러 값들로 집한인 자료구조
단일 또는 다중차원(dimension)으로 구성
인덱스(index)로 값을 접근하는 것이 특징



`타입[] 배열명;`

- `타입`: 각 배열 요소의 타입을 지정

`배열명=new 타입[배열 길이];`

- `new` : 배열 생성을 나타내는 연산자
- 이떄 각 요소의 값은 0으로 초기화

`타입[]배열명=new 타입[배열길이];`

- 배열 선언과 동시에 생성

`타입[]배열명={...};`

- 선언과 동시에 초기화
- `new` 연산자 사용 불필

`타입 배열이름[]=new 타입[배열크기];`

- `[ ]` 를 변수 뒤에 붙여서 배열 표기 가능

---

- 배열의 요소는 인덱스로 접근
    - 인덱스: 0~배열길이-1
- 경계 검사(Boundary Checking)수행
    - Java런타임 시스템이 잘못된 인덱스에 접근하는지 체크

## 2차원 배열

`타입[][]배열이름=new 타입[행][열]`

- 반복문을 통해 접근 가능
- 첫번째 차원(행)크기 명시 필수
    - 두번째 차원의 배열은 개별적으로 생성 가능
    
    ```cpp
    int[][] twoD = new int[4][];
    twoD[0] = new int[5];
    twoD[1] = new int[5];
    twoD[2] = new int[5];
    twoD[3] = new int[5];
    ```
    

`타입[][]배열이름={% raw %}{{...},{...},...}; {% endraw %}`

- 선언과 동시에 초기화
- `new`연산자 불필요

`타입 배열이름[][]=new 타입[행][열];`

- `[ ]` 를 변수 뒤에 붙여서 배열 표기 가능

### 비대칭 2차원 배열 생성

- 각 행의 길이가 다른 2차원 배열 생성 가능
    - 메모리를 최적화하여 사용할 때 유용
        ```cpp
        int[][] twoD = new int[4][];
        twoD[0] = new int[1];
        twoD[1] = new int[2];
        twoD[2] = new int[3];
        twoD[3] = new int[4];
        ```
        ![Untitled 3](https://user-images.githubusercontent.com/98319061/218668210-65b6d4eb-3f55-4d33-8ad1-d642fd627e07.png)
