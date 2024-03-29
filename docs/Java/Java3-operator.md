---
title: 3. Operator
layout: default
#nav_order: 2
parent: Java
#permalink: /1.Java/
---

# 3_operator

>## 목차
>1. [데이터 타입](#연산자) <br>
>2. [변수](#제어문) <br>

# 연산자

> 특정한 연산을 하기 위해 사용하는 기호
> 

## 산술 연산자

- 기본적인 산술 연산을 수행
- **이항/단항**으로 구분

{: .text-center}
| 연산자 | 설명 | 비고 |
| --- | --- | --- |
| + | 덧셈(or 양수) | 이항(단항) |
| - | 뺄셈(or 음수) | 이항(단항) |
| * | 곱셈 | 이항 |
| / | 나눗셈 | 이항 |
| % | 모듈로 연산 | 이항 |
| ++ | 1만큼 증가 | 단항 |
| - - | 1만큼 감소 | 단항 |

- 접두어에 ‘=’를 붙일 시 연산 후 좌변에 대입
    
    {: .text-center}
    | 연산자 | 설명 | 비고 |
    | --- | --- | --- |
    | += | 덧셈후 대입 | 이항 |
    | -= | 뺄셈 후 대입 | 이항 |
    | *= | 곱셈 후 대입 | 이항 |
    | /= | 나눗셈 후 대입 | 이항 |
    | %= | 모듈로 연산 후 대입 | 이항 |

- 피연산자는 숫자 타입
    - boolean타입 사용 불가
- 피연사의 타입이 다를 경우
    - 큰 범위 타입으로 변환 후 연산 수행
- 나눗셈 연산(’/’) 수행 시 소숫점은 무시됨
    
    `double a = 6/4;` → a: 1.5
    
    `int b = 6/4;` → b: 1
    

### 모듈로(modulus) 연산자

- 나눗셈 후 나머지를 취하는 연산
- ‘%’연산자를 사용
- 정수 타입, 부동소수점 타입에 적용가능

### 복합 대입 연산자

- 산술과 대입(assignment)연산자를 조합
- `+=` ,`-=` , …
- 적은 타이핑으로 동일한 연산 가능
- 성능 측면에서 좀 더 효율적

### 증감 연산자

- C언어와 동일하게 ‘++’와 ‘- -’을 이용
- 접두어, 접미어에 따라 다른 의미를 가짐
    
    `y=++x;` → `x=x+1;` → `y=x;`
    
    `y=x++;` → `y=x;` → `x=x+1;`
    

## 비트 연산자

- 비트 단위로 연산을 수행
- 정수 타입에만 적용(long, int, short, char, byte)
- 비트(bit)란?
    - 모든 정수는 이진수로 나타낼 수 있음
    - 각 이진수 숫자(binary digit)를 비트(bit)라고 함

### 2의 보수(two’s complement)

- Java에서 사용하는 이진수 체계
    - 음의 이진수를 2의 보수로 나타냄
    - 최상위 비트0: 양수
    최상위 비트1: 음수
- 2의 보수 구하는 법(-42)
    1. 양수의 이진수를 구함(00101010)
    2. 각 비트를 뒤집고 1을 더함(11010110)
- Why?
    - 1의 보수 체계에는 -0이 존재→ 산술 연산 시 부적합(-0은 수학적으로 존재X)

### 비트 논리 연산자

{: .text-center}
| 연산자 | 설명 |
| --- | --- |
| & | AND |
| \| | OR |
| ^ | XOR |
| ~ | NOT |
 
### 비트 시프트 연산자

- 모든 비트를 왼쪽 or 오른쪽으로 이동
- long, int , short, char, byte타입에 적용

{: .text-center}
| 연산자 | 설명 |
| --- | --- |
| >> | 오른쪽 시프트 |
| >>> | 오른쪽 시프트 후 0으로 채움 |
| >>= | 오른쪽 시프트 후 대입 |
| >>>= | 오른쪽 시프트 후 0으로 채우고 대입 |
| << | 왼쪽 시프트 |
| <<= | 왼쪽 시프트 후 대입 |

**왼쪽 시프트**

`value << num`

- num 횟수만큼 value를 왼쪽으로 시프트
- 왼쪽 num개의 비트 제거
- 제로확장(zero extension): 
오른쪽 num개의 비트를 0으로 채움
- 자동 타입 변환에 유의
    - Java는 모든 연산식 실행 시 int로 간주
    - byte, short타입은 시프트 후 타입 캐스팅 필요

**오른쪽 시프트**

`value >> num`

- num횟수만큼 value를 왼쪽으로 시프트
- 오른쪽 num개의 비트 제거
- 부호 확장(sign extension):
왼쪽 num개의 비트를 최상위비트와 같은 것으로 채움

**비트 시프트 연산 특징**

- $2^n$만큼 값을 변환
- m을 n번 시프트
    
    →왼쪽 시프트: m*$2^n$
    
    →오른쪽 시프트: m*$2^{-n}$
    
- 2의 배수만큼 곱셈/나눗셈 필요시 자주 사용됨

{: .highlight }
💡 최상위비트가 변할 시 부호도 변함


## 비교 연산자

- 두 피연산자를 비교 후 참/거짓 판단
- 조건문, 반복문에서 주로 사용
- 반환값은 boolean타입
- Java는 boolean타입의 true만 참으로 간주
    - C/C++는 0이 아닌 정수는 모두 참으로 간주

{: .text-center}
| 연산자 | 설명 |
| --- | --- |
| == | 같은지 |
| != | 다른지 |
| > | 큰지 |
| < | 작은지 |
| >= | 크거나 같은지 |
| <= | 작거나 같은지 |

## 불리언 논리 연산자

- AND, OR, XOR, NOT의 논리 연산 수행
- boolean타입 만을 피연산자로 취함

{: .text-center}
| 연산자 | 설명 |
| --- | --- |
| & | AND |
| | | OR |
| ^ | XOR |
| ~ | NOT |

```java
boolean a=true;
boolean b = false;
boolean c = a | b;//c:true
```

## 쇼트 서킷 논리 연산자

- C/C++과 같이 쇼트서킷(short-circuit)논리 연산 지원

`A && B`

조건식 A가 false일 경우 조건식 B미수행

`A || B`

조건식 A가 true일 경우 조건식 B미수행

→조건식 A에 따라 빠르게 결정가능

```java
if(denom != 0 && num / denom > 0)
//denom이 0이 아닌 경우 오른쪽 조건문 실행

if(c == 1 & e++ < 100) d = 100;
//조건식이 논리갓을 반환 하므로 &연산자도 사용가능
```

## 대입연산자

`var=expression`

- var의 타입이 expression과 일치해야함
- 연쇄적인 대입 연산도 가능

```java
int x, y, z;
x=y=z=100;
//x, y, z모두 100가짐
```

## 조건 연산자

`연산식1 ? 연산식2 : 연산식3`

- `연산식1`이 true일 때 `연산식2`실행
- false일 때는 `연산식3`실행
- 반환 값은 실행되는 연산식의 결과값
    - 두 연산식은 같은 타입을 반환해야함
    
    `ratio = denom == 0 ? 0 : num / denom;`
    

## 연산자 우선순위

![Untitled](https://user-images.githubusercontent.com/98319061/220035575-37a6d594-c4ca-40fc-8f90-e27ec64d04c7.png)


### 괄호

- 괄호를 이용해 명시적 우선순위 정의 가능

```java
a >> b + 3;//a를 (b+3)만큼 오른쪽 시프트
(a >> b) + 3;//a를 b만큼 오른쪽 시프트 후 3 더하기
```

---

# 제어문

> 제어문(control statement)
> 

프로그램의 실행흐름을 제어하는 것

- 조건문(conditional statement)
- 반복문(iterative statement)
- 분기문(branch statement)

## 조건문

- 조건식에 따라 프로그램의 흐름 제러
- Java는 if와 switch 두가지 조건문 지원

### if-else문

`if(조건식)실행문;
 else 실행문;`

- 실행문은 단일/복합 실행문 모두 가능
    - 복합 실행문 사용시 중괄호 사용
- 조건식의 true, false에 따라 다른 실행문 수행
- 조건식(condition): <br>
조건식에는 비교 연산식, 변수, 논리값 가능
- 중첩된 if 문: if문을 다른 if문 안에 포함시킬 수 있음

{: .highlight }
💡 else는 가장 가까운 if와 매칭됨에 주의


### if-else-if문

`if(조건식)
    실행문;
else if(조건식)
    실행문;
   ...
else
    실행문;`

- 다중 if문을 만들 때 사용

### switch문

`switch(변수){
    case 값1:
        실행문
        break;
    ...
    default:
        실행문
}`

- 여러 실행문 중 조건을 만족하는 하나만을 수행
    - 모든 조건이 비교되는 if-else-if문과의 차이점
- 변수에는 byte, short, int , char, 열거형, String타입이 가능
- default문은 선택사항
- 기존 switch문과 개선된 switch문이 있음
- break문 생략: 여러 case레이블 매칭시 유용

---

## 반복문

- 조건에 따라 반복된 작업을 할때 사용(loop생성)
- for, while, do-while

### while문

`while(조건식){본체실행문}`

- 조건식은 boolean타입을 반환
- 특정 조건을 만족하는지 초점
    - true→본체 실행문
    - false→다음 실행문
- 본체가 없는 while문
    
    `while(++i<--j);//i=j가 될 때까지 반복`
    

### do-while문

`do{본체실행문}while(조건식);`

- 본체를 먼저 실행 후 조건식 검사
- 적어도 한번은 본체를 실행(메뉴 화면 등을 구현할 때 유용)

### for문

`for(초기식;조건식;반복식){본체 실행문}`

- 조건보다는 반복 횟수에 초점
- 초기식→조건식→본체→반복식→본체→…
- 두개이상의 변수를 초기식과 반복식에 사용가능
콤마로 구분
- for문의 일부를 생략가능

### for-each문

`for(타입 변수: 컬렉션){본체 실행문}`

- 기존for문을 개선한 것으로 Java5부터 도입
- 각 컬렉션의 원소를 가져와 변수에 대입

---

## 분기문

- 조건 여부에 관계없이 프로그램의 흐름을 변경
- break, continue, return

### break문

- switch문이나 반복문을 종료하는데 사용
- 가장 안쪽의 루프만 종료
- C의 goto처럼 활용가능:
    - `break 레이블;`
    - 레이블로 지정된 블록을 탈출
    중첩된 블록에서 빠져나올 때 사용
    
    ```java
    boolean t = true;
    first: {
    	second: { 
    		System.out.println("Before");
    		if(t) break first;
    	}
    	System.out.println("Not executed");
    }
    System.out.println("After");
    ```
    

### continue문

- 반복문에서 나머지 실행문을 스킵할 때 사용
- continue가 실행되면 조건식 검사로 넘어감

{: .important }
💡for문은 조건식이 아닌 증감식으로 넘어간다.


![Untitled 1](https://user-images.githubusercontent.com/98319061/220035566-39c4c052-1cad-41d4-aba0-227badf86eba.png)

---
<script src="https://utteranc.es/client.js"
        repo="saranghein/saranghein.github.io"
        issue-term="url"
        label="✨💬✨"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>