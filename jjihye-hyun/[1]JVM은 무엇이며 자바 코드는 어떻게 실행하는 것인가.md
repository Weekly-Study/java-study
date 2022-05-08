# JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가	
## JVM이란 무엇인가
JVM은 'JAVA Virtual Machine'을 줄인 것으로, **자바를 실행하기 위한 가상 컴퓨터**라고 직역된다. 여기서 Virtual Machine는 소프트웨어로 구현딘 하드웨어를 뜻하는 넓은 의미의 용어로 실제 컴퓨터(하드웨어)가 아닌 소프트웨어로 구현된 컴퓨터 즉 컴퓨터 속의 컴퓨터 라고 생각하면 된다.   
자바로 작성된 애플리케이션은 모두 JVM에서만 실행되기 때문에 자바 애플리케이션이 실행되기 위해서는 반드시 JVM이 필요하다. 

<img src="https://mblogthumb-phinf.pstatic.net/20160111_69/rbdi3222_1452510606925S921V_PNG/jvm_exe.png?type=w2" alt="Java애플리케이션과 일반 애플리케이션의 비교" width="500px">

1. 자바언어는 운영체제에 독립적이라는 특징이 있다. 이는 JVM 때문   
 ➡️ 일반 애플리케이션은 OS만 거치고 하드웨어로 전달되기 때문에 OS 종속적이다. 그래서 다른 OS에에서 실행시키기 위해서는 애플리케이션을 그 OS에 맞게 변경해야 한다. 반면, 자바 응용프로그램은 운영체제나 하드웨어가 아닌 자바가상머신(JVM) 하고만 통신하고 JVM이 해당 운영체제가 이해할 수 있도록 자바 응용프로그램으로 전달받은 명령을 변환하여 전달한다. 자바로 작성된 프로그램은 운영체제에 독립적이지만 JVM은 운영체제에 종속적이어서 썬에서는 여러 운영체제에 설치할 수 있는 서로 다른 버전의 JVM을 제공한다.(window용 JVM, Linux용 JVM 등). JVM은 바이트 코드를 특정 컴퓨터에서 사용하는 실행 코드로 해석한다. 

2. 자동 메모리 관리(Gabage Collection)   
가비지컬렉터가 자동으로 메모리를 관리해주기 때문에 프로그래머는 메모리를 따로 관리하지 않아도 된다. 

---

## 컴파일 하는 방법
컴파일이란 사람이 이해하는 언어를 기계어로 바꾸는 과정이다. 자바에서의 컴파일은 자바 소스코드(.java)를 읽어 자바 바이트코드(.class)로 변경하는 것이다.

### 자바 컴파일러(Java compiler)
자바 컴파일러는 자바를 가지고 작성한 자바 소스 코드를 자바 가상 머신이 이해할 수 있는 자바 바이트 코드로 변환합니다. 자바 컴파일러는 자바를 설치하면 javac.exe라는 실행 파일 형태로 설치됩니다.   

<code>
Hello.java 작성 === javac.exe (컴파일) ====> Hello.class 생성(바이트 코드) === java.exe (실행) ====> "Hello, world" 출력
</code>    

--- 

## 실행하는 방법

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F991D064B5AE999D512" alt="자바 프로그램의 실행과정" width="500px">   

1. 자바 컴파일러를 통해 자바 클래스 파일(.java)를 자바바이트코드(.class)로 변환한다.
2. 컴파일된 자바 바이트 코드를 JVM의 클래스로더(Class Loader)에게 전달한다.
3. 클래스 로더를 통해 JVM의 런타임 데이터 영역(Runtime Data area)에 올린다.
4. 로딩된 class파일들은 JVM의 Execution engine을 통해 명령어를 해석한다.
5. 해석된 바이트코드는 Runtime Data Area 에 배치되어 실질적인 수행이 이루어지게 된다. 즉, JVM이 main 메소드를 찾아 한줄한줄씩 읽어나가며 method area, heap area, stack area 등에 세팅하고 실행과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리작업을 수행한다.


### 바이트코드란 무엇인가
바이트코드란 JVM이 이해할 수 있는 기계어로 변환된 자바 소스 코드를 의미한다. 이러한 자바 바이트 코드의 확장자는 .class이다.   
JVM은 바이트코드를 해당 OS의 기계어로 변환하여 OS로 전달한다. 이에 자바 바이트 코드는 자바 가상 머신만 설치되어 있으면, 어떤 운영체제에서라도 실행될 수 있다.

---

## JIT 컴파일러란 무엇이며 어떻게 동작하는가
JIT(Just—In—Time) 컴파일러란 바이트코드(컴파일된 자바코드)를 하드웨어의 기계어로 바로 변환해준다.  

<img src="https://miro.medium.com/max/1400/1*VFo0CC-chzvqJk6sls6ukQ.png" alt="JIT 컴파일러" width="500px">   

JIT 컴파일러는 JRE안에 존재(JVM의 Execution Engine 파트)하면서 프로그램을 실행할 떄 기계어로 번역해 전달한다. JIT 컴파일러를 사용함으로써 인터프리터 속도를 개선할 수 있다. 예전 자바의 인터프리터 방식은 명령어를 하나씩 실행하는 방식으로 중복된 코드가 있어도 라인별로 실행하기 때문에 중복으로 인터프리터 했다. 반면, JIT 컴파일러은 이러한 인터프리터 방식을 보완하기 위해 등장했다. JIT 컴파일러는 실행할 떄 컴파일 하면서 해당 코드를 캐싱한다. 같은 코드를 매번 컴파일 하지 않고 바뀐 부분만 컴파일 하고 나머지는 캐싱했던 코드를 사용한다.

---

## JVM 구성 요소

<img src="https://3553248446-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M5HOStxvx-Jr0fqZhyW%2F-MG6-n2RCnRrss4KBsSz%2F-MG7f7yiI__p7MZ5dcR4%2Fimage.png?alt=media&token=67393c91-2a56-4277-8a88-f2e606f80969" alt="JVM 구성 요소" width="500px">   

### Class Loader
클래스를 JVM의 메모리에 올린다. 즉, 동적로딩(Dynamic Loading)을 통해 필요한 클래스들을 로딩 및 링크하여 런타임 데이터 영역(Runtime Data area) 로드한다.   

**클래스 로더 세부 동작**
1. 로드 : 클래스 파일을 가져와서 JVM의 메모리에 로드한다. 즉, 런타임 데이터 영역에 바이트코드로 배치한다.
2. 검증 : 자바 언어 명세(Java Language Specification) 및 JVM 명세에 명시된 대로 구성되어 있는지 검사한다.
3. 준비 : 클래스가 필요로 하는 메모리를 할당(필드, 메서드, 인터페이스 등등)
4. 분석 : 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경한다.
5. 초기화 : 클래스 변수들은 적절한 값으로 초기화한다.(static 필드)

### Execution Engine
Execution Engine(실행엔진)은 JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행한다. 실행엔진에 의해 기계어로 해석되어 메모리 상(Runtime Data Area)에 배치되게 됩다.
실행엔진에는 Interpreter와 JIT(Just-In-Time) Compiler가 있습니다. 
- Interpreter : 자바 바이트 코드를 한줄 씩 실행. 속도가 느림.
- JIT Compiler : Interpreter의 단점을 보완. 전체 바이트 코드를 컴파일. 속도가 느림. 하지만 캐시 사용으로 한번 컴파일 하면 다음에는 빠르게 수행됨.

### Runtime Data Area
- Stack Area
  - 클래스 내의 메소드에서 사용되는 정보들이 저장되는 공간 
  - 매개변수, 지역변수, 리턴값 등이 저장되며 LIFO(Last In First Out) 방식으로 메소드 실행 시 저장되었다가 실행이 완료되면 제거된다. 임시저장
- Method(Class, Static) Area
  - 클래스와 메소드, 데이터 타입, 멤버(클래스, 인스턴스)변수와 상수(final) 정보 등이 저장되는 공간
- Heap Area
  - new 키워드로 생성된 객체와 배열 등의 참조형 변수정보가 저장되는 공간
  - Method Area에 올라온 클래스들만 생성 가능
  - jdk 8 이상 : static 변수, string 상수 풀
  - GC의 대상
- PC Register Area
  - 쓰레드마다 하나씩 생성. 
  - JVM 명령의 주소값이 저장되는 공간
- Native Method Stack Area
  - 자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역(C/C++ 코드) 

### garbage collector
Heap 메모리 영역에 생성된 객체들 중에 참조되지 않는 객체들을 탐색 후 제거하는 역할을 한다. GC가 수행되는 동안 GC를 수행하는 쓰레드가 아닌 다른 모든 쓰레드가 일시정지된다.

---

## JDK와 JRE의 차이

<img src="https://miro.medium.com/max/636/1*8oNn6HxcWFmrCsgUt27k0w.jpeg" alt="JDK-JRE-JVM 비교" width="500px">   

- JDK: 자발개발도구(Java Development Kit)
  -  JDK = JRE + 개발에 필요한 실행파일(javac.exe 등)
- JRE: 자바실행환경(Java Runtime Environment), 자바로 작성된 응용프로그램이 실행되기 위한 최소환경
  - JRE = JVM + 클래스 라이브러리(Java API)


---
### 참고
http://www.tcpschool.com/java/java_intro_programming   
https://coding-nyan.tistory.com/87    
https://medium.com/@ahn428/java-jit-%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC-c7d068e29f45    
https://incheol-jung.gitbook.io/docs/q-and-a/java/jvm   
https://aljjabaegi.tistory.com/387
https://velog.io/@pond1029/JVM
https://velog.io/@woo00oo/%EC%9E%90%EB%B0%94-%EC%BB%B4%ED%8C%8C%EC%9D%BC-%EA%B3%BC%EC%A0%95