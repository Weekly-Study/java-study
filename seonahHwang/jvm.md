# JVM

# JVM이란 무엇인가

Java Byte Code를 OS에 맞게 해석해주는 역할

자바를 실행하기 위한 가상 기계

역할 : 바이너리 코드를 읽고, 검증하고, 실행한다

byte code는 기계어가 아니어서 os에서 바로 실행되지 않는다.

이 때  JVM은 해석을 거치므로 C언어와 같은 네이티브 언어에 비해속도가 느렸지만

JIT 컴파일러를 구현해 이 점을 극복

# 컴파일 하는 방법

Java Compiler (javac 명령어 실행)에 의해

Java Source (.java 확장자)로 부터 Byte Code (.class 확장자)가 생성된다

```java
// class 파일 생성
$ java main.java
```

# 실행하는 방법

바이트코드 파일을 java.exe로 실행

```java
// 파일 실행
$ java main
```

java.exe 명령어 실행시 JVM은 바이트 코드 파일을 메모리로 로드하고

최적의 기계어로 번역함.

이후 main() 메소드를 찾아 실행시킴

모든 클래스가 main 메서드를 가지고 있어야하는 것은 아니지만

하나의 java 어플리케이션에는 main메서드를 포함한 클래스가 반드시 하나는 있어야한다.

main메서드는 Java 어플리케이션의 시작점이므로 main 메서드 없이는 java 어플리케이션을 실행할 수 없기 때문이다

# 바이트 코드란 무엇인가

하드웨어가 아닌 가상 컴퓨터에서 돌아가는 실행 프로그램을 위한 이진표현법.

하드웨어가 아닌 소프트웨어에 의해 처리되기 때문에

보통 기계어보다 더 추상적

# JIT 컴파일러란 무엇이며 어떻게 동작

interpreter 와 JIT Compiler

`interpreter`

자바 바이트 코드를 한 줄 씩 실행, 여러번 실행하는 환경에서 다소 느림

`JIT Compiler`

Interpreter의 단점을 보완

전체 바이트 코드를 컴파일

캐시 사용으로 한번 컴파일하면 다음에는 빠르게 수행

- JIT 컴파일(just-in-time-compilation)은 프로그램을 실제

실행하는 시점에 기계어로 번역하는 컴파일 기법

- JIT 컴파일러는

실행 시점에서 인터프리트 방식으로 기계어 코드를 생성하면서

그 코드를 캐싱하여 같은 함수가 여러 번 불릴 때 매번 기계어 코드를 생성하는 것 방지

이후에는 바뀐 부분만 컴파일 하고 나머지는 캐싱된 코드 사용

- JIT 컴파일러의 주요 특징은 코드를 컴파일 한 후에 JIT 컴파일러를 실행한다는 것

# JVM 구성 요소

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb65c163-5225-47ce-9856-94c0585184cd/Untitled.png)

# `Class loader`

runtime 시점에 클래스를 로딩하게 해주며

클래스의 인스턴스를 생성하면 클래스 로더를 통해 메모리에 로드하게 된다

JVM 내로 클래스 파일을 로드한다

Runtime 시에 동적으로  Runtime Data Area에 로드

# `Runtime data areas`

JVM이 프로그램을 수행하기 위해 os로부터 별도로 할당받은 메모리 공간.

### Method Area ( = 클래스 영역 = static 영역 = 공유 메모리 영역)

JVM이 시작할 때 생성되고 모든 스레드가 공유하는 영역

클래스 정보를 처음 메모리 공간에 올릴 때 초기화 되는 대상을 저장하기 위한 메모리 공간

### Heap Area

- Runtime에 동적으로 할당되는 데이터가 저장되는 영역

    ex) 참조타입 변수 (객체, 배열)

- Heap에 할당된 데이터는 GC의 대상이다

### Stack Area

각 스레드마다 하나씩 존재

스레드가 시작될 때 할당

메소드 내에서 정의하는 기본자료형에 해당되는 지역변수의 데이터 값이 저장되는 공간

ex) 자바 프로그램에서 추가로 스레드 생성을 안했다면

main 스레드만 존재하므로 JVM 스택도 하나인셈

# `Execution engine`

load된 class의 bytecode를 실행하는 runtime module



# JDK와 JRE의 차이

## JDK (Java Development Kit)

JDK = JRE + a

자바 애플리케이션 개발환경

실행환경, 컴파일러, 디버거 등 자바 앱을 개발하기 위한 도구 포함

(javac, java 등)

## JRE

자바 앱의 실행환경

- 자바 프로그램 실행을 위해 JRE 설치 필수
- 자바 프로그래밍을 하기위해선 JDK 필요
