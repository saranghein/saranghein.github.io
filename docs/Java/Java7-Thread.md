---
title: 7. Thread
layout: default
#nav_order: 2
parent: Java
#permalink: /1.Java/
---

# 7_thread

# 스레드 배경지식

## 프로세스(process)

- 실행 중인 프로그램
    - 디스크에 있는 프로그램이 메모리에 적재된 상태
    - 운영체제의 제어를 받는 상태
- 특징
    - 프로세스는 자신만의 자원을 가짐
    - 프로세스끼리는 서로 독립적

## 스레드(thread)

- 하나의 프로그램 실행 흐름
    - 프로세스 내부에 존재
    - 프로세스는 적어도 하나의 스레드를 가짐
- 특징
    - 프로세스에 비해 필요 자원이 적음
    - 경량 프로세스
    - 스레드 간 자원을 공유
    
    ![Untitled](7_thread%2035deece598b34cd1a3a5d61a0f9b64c9/Untitled.png)
    

## 멀티 태스킹(multitasking)

- 운영체제가 여러 작업을 동시에 실행
    - 시스템 자원의 효율적 사용이 목적
- 프로세스 기반 멀티 태스킹
    - 다수 프로세스를 동시에 실행하는 것
    vi 에디터와 웹 브라우저 동시 실행
- 스레드 기반 멀티 태스킹
    - 단일 프로세스가 여러 작업을 동시에 실행하는 것
    VI에디터에서 텍스트 출력과 입력 동시 진행

## Java의 멀티 태스킹

- 스레드 기반 멀티 태스킹 사용→멀티스레딩
    - Java애플리케이션 실행 시 하나의 프로세스 실행
    - 프로세스 내에서 여러 스레드 실행 가능
- 언어 레벨에서 멀티 스레딩 구현

	![Untitled 1](https://user-images.githubusercontent.com/98319061/221090324-75a27656-1b91-43c0-9905-3176cd747a25.png)

### 멀티스레딩의 장점

- 유휴시간(idle time)의 최소화
    - 한 작업이 끝날 때까지 기다려야 할 때
    - 네트워크나 인터랙티브 프로그램에서 자주 발생
- 예제:
    - 네트워크 트래픽 전송시간>CPU처리시간
    - 사용자 텍스트 입력시간>버퍼 처리 시간

## 전통적인 스레드 모델

- 동기삭(synchronous)스레드 모델
    - 이베느 루프(event loop)와 폴링(polling) 사용
    - 스레드는 루프를 돌며 이벤트 큐를 검사
- 단점
    - 스레드 블록 시 프로그램 전체가 정지
    
    ![[https://medium.com/@tigranbs/concurrency-vs-event-loop-vs-event-loop-concurrency-eb542ad4067b](https://medium.com/@tigranbs/concurrency-vs-event-loop-vs-event-loop-concurrency-eb542ad4067b)](https://user-images.githubusercontent.com/98319061/221090328-9ba2a9ba-5730-4758-b095-2656f351e1f0.png))
    
    [https://medium.com/@tigranbs/concurrency-vs-event-loop-vs-event-loop-concurrency-eb542ad4067b](https://medium.com/@tigranbs/concurrency-vs-event-loop-vs-event-loop-concurrency-eb542ad4067b)
    

## Java의 스레드 모델

- 비동기식(asynchronous)모델
    - 스레드의 블록이 다른 스레드에 영향X
    
    ![[https://subscription.packtpub.com/book/application-development/9781785883248/1/ch01lvl1sec10/android-thread-model](https://subscription.packtpub.com/book/application-development/9781785883248/1/ch01lvl1sec10/android-thread-model)](https://user-images.githubusercontent.com/98319061/221090329-c4d6a85b-3d55-40a2-813a-ebb6f40b7bb4.png))
    
    [https://subscription.packtpub.com/book/application-development/9781785883248/1/ch01lvl1sec10/android-thread-model](https://subscription.packtpub.com/book/application-development/9781785883248/1/ch01lvl1sec10/android-thread-model)
    

### Java와 CPU 코어

- Java는 싱글/멀티 코어 시스템에서 모두 동작
- 싱글 코어 CPU
    - 다수 스레드가 1개의 CPU를 공유
    - 실제로 병렬 처리는 안됨
- 멀티 코어CPU
    - 실제로 스레드를 여러 코어에서 병렬처리

### Java의 스레드 상태

![Untitled 4](https://user-images.githubusercontent.com/98319061/221090330-6ec8ab55-11ad-49a0-924c-28e2fdd78252.png)

## Java의 동기화

- 때로는 동가화가 필요한 경우가 있음
데이터 구조 공유, 스레드 간 통신
- Java는 모니터(monitor)메커니즘을 이용
- 모니터:
    - 스레드 간 상호배제(mutual exclusion)를 구현하는 동기화 구조
    - 모든 오브젝트에 구현되어 있음

### 모니터 동작 원리

- 스레드가 오브젝트 조작 시 모니터 확보 필요
    - 스레드가 모니터를 가지면 오브젝트에 락을 설정
    - 다른 스레드는 해당 오브젝트에 접근 불가
    
    ![[https://www.artima.com/insidejvm/ed2/threadsynch.html](https://www.artima.com/insidejvm/ed2/threadsynch.html)](https://user-images.githubusercontent.com/98319061/221090332-d0fc7d0f-efcc-488c-92c0-eb273429e151.png))
    
    [https://www.artima.com/insidejvm/ed2/threadsynch.html](https://www.artima.com/insidejvm/ed2/threadsynch.html)
    

---

# Java 스레드

## Main스레드

- Java프로그램 시작 시 실행되는 기본 스레드
    - Main스레드를 기점으로 자식 스레드가 생성
    - 프로그램 종료 직전까지 실행되는 마지막 스레드
    
    ![Untitled 6](https://user-images.githubusercontent.com/98319061/221090335-9ef5e544-6b9b-4fce-b394-06e5c5f4064b.png)

    

### 스레드 확인해보기

`static Thread currentThread()`

- 모든 스레드는 Thread오브젝트로 제어
- 현재 스레드는 다음 메서드로 접근 가능
    - 현재 실행 스레드의 오브젝트 참조를 반환
    
    ```cpp
    //CurrentThreadDemo.java
    class CurrentThreadDemo {
    	public static void main(String[] args) {
    		Thread t = Thread.currentThread();
    		System.out.println("Current thread: " + t);
    	}
    }
    //>>Current thread: Thread[main,5,main]
    ```
    

## 다른 스레드 생성하기

![Untitled 7](https://user-images.githubusercontent.com/98319061/221090336-9ccaee2e-203f-4231-a585-252fca02e954.png)

### 1. Runnable 인터페이스

- 클래스가 Runnable인터페이스를 구현하는 방법
- `public boid run()`을 멤버 메서드로 가짐
    - `run()`내부에 스레드가 실행할 코드 작성
    
    ```cpp
    class MuFunnable implements Runnable{
    	public void run(){
    		//스레드가 실행할 코드
    	}
    }
    ```
    
- 스레드 실행
    - Runnable 구현 클래스를 스레드 오브젝트로 생성
    - 이후 `start()` 메서드를 통해 스레드 실행
    
    ```cpp
    //Runnable구현클래스인 MyRunnable객체이다.
    Thread thread=new Thread(**new MyRunnable()**);
    thread.start();//스레드 실행
    ```
    
    ```cpp
    //NewThread.java
    class NewThread **implements Runnable** {
    	Thread t;
    	NewThread() {
    		**t = new Thread(this);**
    		System.out.println("Child thread: " + t);
    	}
    	public void run() {
    		try {
    			for(int i = 5; i > 0; i--) {
    				System.out.println("Child Thread: " + i);
    				Thread.sleep(500);
    			}
    	} catch (InterruptedException e) {
    			System.out.println("Child interrupted.");
    	}
    		System.out.println("Exiting child thread.");
    	}
    }
    
    class ThreadDemo {
    	public static void main(String[] args) {
    		try {
    			**NewThread nt = new NewThread();
    			nt.t.start();**
    			for(int i = 5; i > 0; i--) {
    				System.out.println("Main Thread: " + i);
    				Thread.sleep(1000);
    			}
    		} catch (InterruptedException e) {
    			System.out.println("Main thread interrupted.");
    		}
    		System.out.println("Main thread exiting.");
    	}
    }
    ```
    

### 2. Thread 클래스

- Thread클래스를 상속하는 방법
- `run()` 에 스레드 실행 코드 구현

```cpp
class MyThread extends Thread{//Thread의 자식 클래스
	public void run(){//Thread클래스의 run()메서드를 오버라이딩한다.
		//스레드가 실행할 코드
	}
}
```

- Thread클래스 멤버
    
    
    | 생성자 | 설명 |
    | --- | --- |
    | Thread() | 스레드 객체를 생성 |
    | Thread(Runnable target) | Runnable구현 객체를 사용해 스레드 객체를 생성 |
    | Thread(Runnable target, String name) | Runnable구현 객체를 사용해 스레드 이름이 name인 스레드 객체를 생성 |
    
    | 메서드 및 상수 | 설명 |
    | --- | --- |
    | static Thread currentThread() | 현재 실행 중인 스레드 객체의 참조 값을 반환 |
    | String getName() | 스레드의 이름 반환 |
    | int getPriority() | 스레드의 우선순위 값을 반환 |
    | boolean isInterrupted() | 스레드가 인터럽트를 당했는지 여부 반환 |
    | void setName() | 스레드의 이름을 설정 |
    | void setPriority() | 스레드의 우선순위 설정 |

```cpp
//NewThread.java
class NewThread **extends Thread** {
	NewThread() {
		**super();**
		System.out.println("Child thread: " + this);
	}
	public void run() {
		try {
			for(int i = 5; i > 0; i--) {
				System.out.println("Child Thread: " + i);
				Thread.sleep(500);
			}
		} catch (InterruptedException e) {
			System.out.println("Child interrupted.");
		}
		System.out.println("Exiting child thread.");
	}
}

class ExtendThread {
	public static void main(String[] args) {
		**NewThread nt = new NewThread(); 
		nt.start();**
		try {
			for(int i = 5; i > 0; i--) {
				System.out.println("Main Thread: " + i);
				Thread.sleep(1000);
			}
		} catch (InterruptedException e) {
			System.out.println("Main thread interrupted.");
		}
		System.out.println("Main thread exiting.");
	}
}
```

---

| Runnable 인터페이스 사용 | Thread 클래스 사용 |
| --- | --- |
| run() 메서드만 구현하면 될 때 | run() 외 메서드를 오버라이딩 할 필요가 있을 때 |
| 다른 클래스를 상속해야할 때 |  |

---

### `isAlive()` 와 `join()`

- main스레드가 마지막에 종료되도록 보장

`final boolean isAlive()`

- 스레드가 실행 중일 때 true or false

`final void join() throws InterruptedException`

- 특정 스레드가 종료할 때까지 기다림

```cpp
//DemoJoin.java
class NewThread implements Runnable {
	String name; 
	Thread t;
	NewThread(String threadname) {
		name = threadname;
		t = new Thread(this, name);
		System.out.println("New thread: " + t);
	}
	public void run() {
		try {
			for(int i = 5; i > 0; i--) {
				System.out.println(name + ": " + i);
				Thread.sleep(1000);
			}
		} catch (InterruptedException e) {
			System.out.println(name + " interrupted.");
		}
		System.out.println(name + " exiting.");
	}
}

class DemoJoin {
	public static void main(String[] args) {
		NewThread nt1 = new NewThread("One");
		nt1.t.start();
		System.out.println("Thread One is alive: "+ **nt1.t.isAlive()**);
		try {
			**nt1.t.join();**
		} catch (InterruptedException e) {
			System.out.println("Main thread Interrupted");
		}
		System.out.println("Thread One is alive: "+ **nt1.t.isAlive()**);
		System.out.println("Main thread exiting.");
	}
}
/*>>
New thread: Thread[One,5,main]
Thread One is alive: true
One: 5
One: 4
One: 3
One: 2
One: 1
One exiting.
Thread One is alive: false
Main thread exiting.
*/
```

## 스레드 우선순위

- 스케줄러가 어떤 스레드를 우선시할지 결정할때(어떤 스레드를 CPU에 돌릴까?)
- 우선 순위가 높은 스레드는 낮은 스레드를 선점함
높은 우선 순위를 갖는 스레드가 더 자주 CPU사용

### 스레드 우선순위 설정

`final void setPriority(int level)`

- `level` 은 스레드의 우선순위
- Thread클래스에서 아래 상수를 제공
    
    
    | 우선순위 상수 | 설명 |
    | --- | --- |
    | MAX_PRIORITY | 최고 우선순위인 10 |
    | NORM_PRIORITY | 중간 우선순위인 5 |
    | MIN_PRIORITY | 최저 우선순위인 1 |

### 스레드 동기화

- 두개 이상의 스레드가 공유 자원을 접근시
하나의 스레드만 자원을 사용하도록 보장 필요
- Java는 언어레벨에서 동기화 지원→`synchronized` 키워드 사용
- 레이스 컨디션(race condition):
동기화가 설정 안되면 발생하는 문제

```cpp
//Synch.java
class Callme {
	void call(String msg) {
		System.out.print("[" + msg);
		try {
			Thread.sleep(1000);
		} catch(InterruptedException e) {
			System.out.println("Interrupted");
		}
		System.out.println("]");
	}
}

class Caller implements Runnable {
	String msg;
	Callme target;
	Thread t;
	public Caller(Callme targ, String s) {
		target = targ;
		msg = s;
		t = new Thread(this);
	}
	public void run() {
		target.call(msg);
	}
}

class Synch {
	public static void main(String[] args) {
		Callme target = new Callme();
		Caller ob1 = new Caller(target, "Hello");
		Caller ob2 = new Caller(target, "World");
		ob1.t.start();
		ob2.t.start();
		try {
			ob1.t.join();
			ob2.t.join();
		} catch(InterruptedException e) {
			System.out.println("Interrupted");
		}
	}
}
/*>>
[World[Hello]
]
*/
/*>>
[Hello[World]
]
*/
```

→ `call()` 에 대해 레이스 컨디션이 발생

### 동기화 메서드

- 오브젝트 코드에 임계영역을 설정할 때 사용
    - 스레드가 임계영역에 진입 시 락을 설정
    - 다른 스레드는 락이 풀릴 때 까지 대기
    
    ```cpp
    public synchronized void 메서드(){
    	//임계영역 코드
    }
    ```
    

```cpp
//Synch.java 수정
class Callme {
	**synchronized** void call(String msg) {
		System.out.print("[" + msg);
		try {
			Thread.sleep(1000);
		} catch(InterruptedException e) {
			System.out.println("Interrupted");
		}
		System.out.println("]");
	}
}
```

### 동기화 블록

- 동기화 메서드는 클래스 내부 코드 접근 필요
    - 써드 파티 클래스는 사용할 수 없음
    
    ```cpp
    synchronized(공유객체){
    	//임계영역 코드
    }
    ```
    
- 오브젝트 참조자로 동기화 설정 가능
    - 설정된 블록은 임계영역으로 간주됨

```cpp
//Synch1.java
class Callme {
	void call(String msg) {
		System.out.print("[" + msg);
		try {
			Thread.sleep(1000);
		} catch (InterruptedException e) {
			System.out.println("Interrupted");
		}
		System.out.println("]");
	}
}

class Caller implements Runnable {
	String msg;
	**Callme target;**
	Thread t;
	public Caller(Callme targ, String s) {
		target = targ;
		msg = s;
		t = new Thread(this);
	}
	public void run() {
		**synchronized(target) {
			target.call(msg);
		}**
	}
}

class Synch1 {
	public static void main(String[] args) {
		Callme target = new Callme();
		Caller ob1 = new Caller(target, "Hello");
		Caller ob2 = new Caller(target, "World");
		ob1.t.start();
		ob2.t.start();
		try {
			ob1.t.join();
			ob2.t.join();
		} catch(InterruptedException e) {
			System.out.println("Interrupted");
		}
	}
}
```

## 스레드 간 통신

- 생산자-소비자문제:
공유 자원을 생산하고 소비하는 두 스레드 간 어떻게 협업을 할 것인가
- 임계 영역 접근에 대한 스레드 간 통신이 필요
    - Java는 Object클래스에 관련 메서드를 지원

| wait() | 호출자 스레드가 락을 포기하고 잠듦 |
| --- | --- |
| notify() | wait() 를 호출한 스레드 중 하나를 깨움 |
| notifyAll() | wait() 를 호출한 모든 스레드를 깨움 |

```cpp
//PC.java
class Q {
	int n;
	**synchronized** int get() {
		System.out.println("Got: " + n);
		return n;
	}
	**synchronized** void put(int n) {
		this.n = n;
		System.out.println("Put: " + n);
	}
}

class **Producer** implements Runnable {
	Q q;
	Thread t;
	Producer(Q q) {
		this.q = q;
		t = new Thread(this, "Producer");
	}
	public void run() {
		int i = 0;
		while(true)
			**q.put(i++);**
	}
}

class **Consumer** implements Runnable {
	Q q;
	Thread t;
	Consumer(Q q) {
		this.q = q;
		t = new Thread(this, "Consumer");
	}
	public void run() {
		while(true)
			**q.get();**
	}
}
/*
Put: 1
Got: 1
Got: 1
Got: 1
Got: 1
Got: 1
Put: 2
Put: 3
Put: 4
…
*/
```

```cpp
//PC.java 수정
class Q {
	int n;
	**boolean valueSet = false;**
	synchronized int get() {
		try {
			if(**!valueSet**)
				**wait();**
		} catch(InterruptedException e) {
			System.out.println("InterruptedException");
		}
		System.out.println("Got: " + n);
		**valueSet = false;
		notify();**
		return n;
	}

	synchronized void put(int n) {
		try {
			if(**valueSet**)
				**wait();**
		} catch(InterruptedException e) {
			System.out.println("InterruptedException");
		}
		this.n = n;
		**valueSet = true;**
		System.out.println("Put: " + n);
		**notify();**
	}
}
```

## 데드락(deadlock)

- 두 스레드가 공유자원에 대해 서로 기다리는 상태
    - 스레드가 영원히 대기상태에 빠짐
- 멀티스레딩 환경에서 발생할 수 있는 대표적 문제
    - 단, 확률적으로 발생하기 때문에 디버깅이 어려움
    
    ![Untitled 8](https://user-images.githubusercontent.com/98319061/221090337-f411f825-b8ab-4400-9505-892d39b905fe.png)

    

```cpp
//Deadlock.java
class A {
	**synchronized** void foo(B b) {
		String name = Thread.currentThread().getName();
		System.out.println(name + " entered A.foo");
		System.out.println(name + " call B.last()");
		**b.last();**
	}
	synchronized void last() {
		System.out.println("Inside A.last");
	}
}

class B {
	**synchronized** void bar(A a) {
		String name = Thread.currentThread().getName();
		System.out.println(name + " entered B.bar");
		System.out.println(name + " call A.last()");
		**a.last();**
	}
	synchronized void last() {
		System.out.println("Inside B.last");
	}
}

class Deadlock implements Runnable {
	A a = new A();
	B b = new B();
	Thread t;
	Deadlock() {
		Thread.currentThread().setName("MainThread");
		t = new Thread(this, "RacingThread");
	}
	public void run() {
		b.bar(a); // get lock on b in other thread.
		System.out.println("Back in other thread");
	}
	void deadlockStart() {
		t.start();
		a.foo(b); // get lock on a in this thread.
		System.out.println("Back in main thread");
	}
	public static void main(String[] args) {
		Deadlock dl = new Deadlock();
		dl.deadlockStart();
	}
}
```

## 스레드 라이프 사이클

- 스레드가 스케줄링 될 때 따르는 흐름
    - 각 흐름에 따라 상태가 변경
    
    ![Untitled 9](https://user-images.githubusercontent.com/98319061/221090339-7349a4fd-5fc6-4cff-a9c5-1689cb7f876e.png)

    

### 스레드 상태

- java는 스레드 상태를 상수로 관리
    - Thread클래스에 정의
    
    | 상태 | 상수 | 설명 |
    | --- | --- | --- |
    | 객체 생성 | NEW | 객체를 생성한 후 아직 시작하지 않은 상태 |
    | 실행대기 | RUNNABLE | 실행 준비가 된 상태 |
    | 중지 | BLOCKED | 입출력 등 락(Lock)이 풀릴 때 까지 기다리는 상태 |
    |  | WAITING | 다른 스레드가 통지할 때까지 기다리는 상태 |
    |  | TIME_WAITING | 주어진 시간동안 기다리는 상태 |
    | 종료 | TERMINATED | 실행을 마친 상태 |

### 스레드 상태 조작 메서드

- 스레드 상태 조작을 위한 다양한 메서드 제공

| 메서드 | 설명 |
| --- | --- |
| void interrupt() | 실행 중인 스레드에 인터럽트를 걸어 중지시킴 |
| void join() | 주어진 시간이 지나거나 대응하는 스레드가 종료될 때까지 대기시킴 |
| void resume() | 중지 상태의 스레드를 실행 대기 상태로 전환시킴 |
| static void sleep() | 주어진 시간 동안 중지 |
| void start() | 스레드를  실행 대기시킴 |
| void stop() | 스레드 종료 |
| void suspend() | 스레드 중지 |
| static void yield() | 우선순위가 동일한 스레드에 실행을 양보 |