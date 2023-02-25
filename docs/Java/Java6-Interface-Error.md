---
title: 6. Interface & Error
layout: default
#nav_order: 2
parent: Java
#permalink: /1.Java/
---

# 6_interface_error

# 인터페이스

- 클래스의 인터페이스를 설계할 때 이용
    - 추상 클래스와 유사한 역할
    - but… 상속과는 별개로 취급
- 클래스에서 구현될 추상메서드 선언
    - 일반 메서드는 정의 불가(but… JDK8부터는 디폴트 메서드 허용)
    - 인스턴스 변수는 선언 불가(static, final변수는 허용)
- 인터페이스 선언
    
    ```cpp
    접근자 interface 인터페이스_이름{
    	//상수 필드
    	//추상 메서드
    
    	//static메서드 ->JDK8부터 가능
    	//default메서드->JDK8부터 가능
    	//private메서드->JDK8부터 가능
    }
    ```
    
- 인터페이스 내부 변수, 메서드의 키워드는 생략
    - 컴파일 시 자동으로 추가됨
    - 변수는 상수: `int MAX=10;` → `public static final int MAX=10;`
    메서드는 추상 메서드: `void func();` → `public abstract void func();`
- `extends` 이용해 인터페이스가 다른 인터페이스 상속가능
- 인터페이스 구현
    
    `class 클래스_명 implements 인터페이스1,2,...{//abstract메서드 구현}`
    
    - 인터페이스에 선언 된 추상 메서드는 모두 구현되어야 함
    - 여러 인터페이스 상속 가능
    - 구현 시 추가로 메서드 정의 가능

### 인터페이스와 오브젝트 참조

- 인터페이스로 구현 클래스 오브젝트 참조가능
    - 상속의 다형성과 유사
- 인터페이스에 선언된 메서드만 참조 가능
    - `Figure f=new Rectangle(10,20); f.area();`

### 인터페이스와 변수 선언

- 인터 페이스 내 선언 되는 변수는 상수로 취급
    - 즉, 상속 후에 변경 불가
- 여러 클래스에서 사용하는 상수를 정의할 때 편리

| 분류 | 인터페이스 | 추상 클래스 |
| --- | --- | --- |
| 구현 메서드 | 포함 불가(단 디폴트 메서드와 정적 메서드는 예외) | 포함 가능 |
| 인스턴스 변수 | 포함 불가 | 포함가능 |
| 다중 상속 | 가능 | 불가 |
| 디폴트 메서드 | 선언 가능 | 선언 불가 |
| 생성자와 main() | 선언 불가 | 선언 가능 |
| 상속에서의 부모 | 인터페이스 | 인터페이스, 추상클래스 |
| 접근 범위 | 모든 멤버를 공개 | 추상메서드를 최소한 자식에게 공개 |

### 중첩 인터페이스

- 클래스 내부에 인터페이스가 선언될 때
- 중첩 인터페이스를 멤버로 둔 클래스 이름을 명시

```cpp
class A {
	**public interface NestedIf {**
		boolean isNotNegative(int x);
	}
}

class B implements **A.NestedIF** {
	public boolean isNotNegative(int x) {
		return x < 0? false: true;
	}
}
//…
**A.NestedIf** nif = new B();
```

### default메서드

- 인터페이스 내 메서드 구현을 정의(JDK8~)
- 장점
    - 호환성을 유지하며 새기능을 추가할 때
    - 클래스에서 구현할 필요 없는 메서드가 있을 때
    
    ![Untitled](https://user-images.githubusercontent.com/98319061/221090007-abf906b4-c770-48a9-b234-104c30063bf8.png)

    
    ```cpp
    public interface MyIF {
    	int getNumber();
    	**default** String getString() {
    		return “default string”;
    	}
    }
    
    class MyIFImp implements MyIF { 
    	public int **getNumber()** { 
    		return 100; 
    	} 
    }
    //…
    
    MyIFImp obj = new MyIFImp(); 
    
    obj.getNumber();//구현없이 호출가능
    obj.getString();
    ```
    

### static메서드

- 인터페이스 내에 static 메서드를 정의할 때(JDK8~)

```cpp
public interface MyIF {
	static int getDefaultNumber() {
		return 0;
	}
}
//..
MyIf.getDefaultNumber();
```

### private메서드

- 인터페이스 내에 private메서드를 정의할 때
- default메서드가 내부적으로 호출할 때 유용

```cpp
interface IntStack { 
//…
	default int[] popNElements(int n) {
		return getElements(n);
	} 
	default int[] skipAndPopNElements(int skip, int n) {
		getElements(skip);
		return **getElements(n);//중복된 구현을 줄일 수 있음**
	}
	**private** int[] getElements(int n) {
		int[] elements = new int[n];
			for(int i=0; i < n; i++) elements[i] = pop();
		return elements;
	}
}
```

---

## 예외처리

### 예외(exception)

- 프로그램 실행 중 발생하는 오류
    - 개발자가 직접 처리해줘야함
    - 예외 발생을 위한 우회 경로 구축 필요

### 예외 타입

- Java에서 모든 예외는 Throwable 클래스를 상속
(2개의 서브 클래스로 구분)

![Untitled 1](https://user-images.githubusercontent.com/98319061/221089996-0192b765-b48e-4f20-aba5-6123e50b11e2.png)


> Error
> 

개발자가 처리할 수 없는 오류
예: 스택 오버플로우, JVM자원 부족

> Exception
> 

개발자가 처리할 수 있는 오류
예: 0으로 나누기, 배열 밖 접근
비검사형 예외(실행 예외) & 검사형 예외(일반예외)

### 비검사형 예외(실행 예외)

- 예외 처리를 하지 않아도 컴파일이 가능한 예외
(개발자의 실수로 발생할 수 있음)

| 실행 예외 | 발생이유 |
| --- | --- |
| ArithmeticException | 0으로 나누기와 같은 부적절한 산술연산을 수행할 때 발생한다. |
| IllegalArgumentException | 메서드에 부적절한 인수를 전달할 때 발생한다. |
| IndexOutOfBoundsException | 배열, 벡터 등에서 범위를 벗어난 인덱스를 사용할 때 발생한다. |
| NoSuchElementException | 요구한 원소가 없을 때 발생한다. |
| NullPointerException | null값을 가진 참조 변수에 접근할 때 발생한다. |
| NumberFormatException | 숫자로 발꿀 수 없는 문자열을 숫자로 변환하려 할 때 발생한다. |

`java.lang.산술연산에 관련된 예외/간량한 이유at스택트레이스(소스행번호)`

`java.lang.ArithmeticException:/by zero at Zero.main(Zero.java:4)`

### 검사형 예외(일반 예외)

- 예외 처리를 하지 않으면 컴팡리 오츄가 발생
    - 예외 처리 코드를 반드시 추가해 줘야함
    
    | 일반예외 | 발생이유 |
    | --- | --- |
    | ClassNotFoundException | 존재하지 않는 클래스를 사용하려 할때 발생 |
    | InterruptedException | 인터럽트되었을 때 발생 |
    | NoSuchFieldException | 클래스가 명사한 필드를 포함하지 않을 때 발생 |
    | NoSuchMethodException | 클래스가 명시한 메서드를 포함하지 않을 때 발생 |
    | IOException | 데이터 읽기 같은 입출력 문제가 있을 때 발생 |

### Java의 예외 처리 방식

- 예외 발생 시 해당 예외를 담은 오브젝트 생성
    - 예외를 생성한 메서드가 잡거나(`catch`)
    - 다른 메서드로 던질 수 있음(`throws`)
    
    ![Untitled 2](https://user-images.githubusercontent.com/98319061/221089999-1edddae0-db7a-4b9b-ab66-4bbe78d21d98.png)

    
- Java 런타임 시스템이 프로그램을 종료시킴
    - 적절한 예외 처리로 예기치 못한 종료를 방지하는 것이 중요!
    
    ![Untitled 3](https://user-images.githubusercontent.com/98319061/221090002-3a524e3e-9b71-4d95-bb7f-3e5d85f8987e.png)

    

```cpp
try{
	//예외 발생 구간
}catch(예외클래스1 매개변수){//매개변수로 정의된 예외클래스만 잡히게 됨
	//핸들러
}
```

### 예외 출력

- Throwable 클래스는 `toString()`을 오버라이딩
    
    `println()` → 호출 되어 예외 출력 
    
    ```cpp
    catch (ArithmeticException e) {
    	System.out.println(“Exception: “ + e);
    }
    //>>Exception: java.lang.ArithmeticException: / by Zero
    ```
    
- 출력 시 사용하는 주요 메서드
    
    
    | 메서드 | 설명 |
    | --- | --- |
    | public String getMessage() | Throwable 객체의 자세한 메시지를 반환 |
    | public String toString() | Throwable 객체의 간단한 메시지를 반환 |
    | public boid printStackTrace() | Throwable rorcpdhk 추적정보를 콘솔 뷰에 출력 |
- 다중 catch 문
    
    ```cpp
    try{
    	//예외 발생 구간
    }catch(예외클래스1매개변수){
    	//핸들러
    }catch(예외클래스2매개변수){
    	//핸들러
    }
    ```
    
    ```cpp
    try {
    	int a = 0;
    	int b = 42 / a;
    	int[] c = { 1 };
    	c[42] = 99;
    } catch(ArithmeticException e) {
    	System.out.println("Divide by 0: " + e);
    } catch(ArrayIndexOutOfBoundsException e) {
    	System.out.println("Array oob: " + e);
    }
    ```
    
    - 상속 관계를 고려한 catch문 정의 필요
        - 항상 서브 클래스가 슈퍼 클래스보다 먼저 와야함
        - 슈퍼 클래스는 서브 클래스 예외를 모두 잡기 때문
        
        ![Untitled 4](https://user-images.githubusercontent.com/98319061/221090005-60d0d8c1-988c-4eb8-853b-1db06f34b8db.png)

        
        ```cpp
        try {
        	int a = 0;
        	int b = 42 / a;
        } catch(**Exception e**) {//서브 클래스 예외를 모두 잡음
        	System.out.println("Generic catch.");
        } catch(ArithmeticException e) { 
        	**// ERROR - unreachable**
        	System.out.println(”Never reached.");
        }
        ```
        
- throw문
    
    `throw 예외_오브젝트;`
    
    - 프로그램이 예외를 직접 발생시킬 때
    - 예외 오브젝트는 Throwable 타입이어야함
    
    ```cpp
    try {
    	throw new NullPointerException("demo");
    } catch(NullPointerException e) {
    	System.out.println("Caught.");
    	throw e;
    }
    ```
    
    ```cpp
    class ThrowsDemo {
    	static void throwOne() {
    		**throw new IllegalAccessException("demo");
    //예외를 생성했으나 아무도 처리안하면 컴파일 에러가 발생함에 유의**
    	}
    	public static void main(String[] args) {
    		throwOne();
    	}
    }
    ```
    
- throws문
    - 호출자(caller)로 예외처리(직접 예외 처리가 어려울 경우)
    - 메서드 선언문에 넘길 예외를 명시
    
    ```cpp
    public void write(String filename)
    	**throws IOException, ArithmeticException**
    //…
    class ThrowsDemo {
    	static void throwOne() **throws IllegalAccessException** {
    		**throw new IllegalAccessException("demo");**
    	}
    	public static void main(String[] args) {
    		try {
    			throwOne();
    		} catch (IllegalAccessException e) {
    			//…
    		}
    	}
    }
    ```
    
- finally블록
    - 예외가 발생 여부와 관계없이 실행되는 블록
        - catch문에 예외가 매칭되지 않아도 실행됨
    - 반드시 실행되어야 하는 코드에 적용(열었던 파일, 소켓 닫기)
    
    ```cpp
    try {
    	int a = 0;
    	int b = 10 / a; 
    } catch (ArithmeticException e) {
    	System.out.println(“Caught”)
    finally {
    	System.out.println(”Finally");
    }
    //>>Caught Finally
    ```
    
- try-with-resouces
    - try 문 내부에 사용된 자원을 자동으로 릴리즈(JEK7~)
    
    ```cpp
    try(자원({
    	//...
    }catch(예외클래스1매개변수){
    	//...
    }
    //...
    ```
    
- 개선된 다중 catch문
    - catch문에서 OR논리 연산자 사용(JDK7~)
        - catch문이 길어지는 걸 방지
        
        ```cpp
        try {
        	int result = a / b; 
        	vals[10] = 19; 
        } catch(ArithmeticException | ArrayIndexOutOfBoundsException e) {
        	//…
        }
        ```

---
<script src="https://utteranc.es/client.js"
        repo="saranghein/saranghein.github.io"
        issue-term="url"
        label="✨💬✨"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>