# JVM이 하는 역할
JVM(Java Virtual Machine)은 자바 프로그램을 실행하기 위해 물리적 머신과 유사하게 소프트웨어로 구현한 것이다. 즉, Java 바이트코드를 실행하는 기계(프로그램)입니다.

1. 자바 프로그램 운영체제에 독립적으로 실행   
JVM은 바이트 코드를 특정 컴퓨터에서 사용하는 실행 코드로 해석합니다.   

<img src="https://mblogthumb-phinf.pstatic.net/20160111_69/rbdi3222_1452510606925S921V_PNG/jvm_exe.png?type=w2" alt="Java애플리케이션과 일반 애플리케이션의 비교" width="400px">

- 자바언어는 운영체제에 독립적이라는 특징이 있다. 이는 JVM 때문   
 ➡️ 일반 애플리케이션은 OS만 거치고 바로 하드웨어로 전달되기 때문에 OS 종속적이다. 그래서 다른 OS에에서 실행시키기 위해서는 애플리케이션을 그 OS에 맞게 변경해야 하는 작업이 필요합니다.   반면, 자바 응용프로그램은 중간에 자바가상머신(JVM) 하고만 통신하고 JVM이 해당 운영체제가 이해할 수 있도록 자바 응용프로그램으로 전달받은 명령을 변환하여 전달합니다. 그렇기 때문에 Java에서는 다른언어와 달리 JVM을 사용하기 때문에 각자의 플랫폼에 맞게끔 컴파일을 따로따로 해줘야 할 필요가 없습니다. 하나의 바이트 코드로 JVM이 설치되어 있는 모든 플랫폼에서 동작이 가능합니다. 
 JVM은 운영체제에 종속적이어서 썬에서는 여러 운영체제에 설치할 수 있는 서로 다른 버전의 JVM을 제공한다.(window용 JVM, Linux용 JVM 등). 
- WORA(Write Once Run Anywhere): 한번 작성하면 어디서든 실행된다.

2. 자동 매모리 관리
자바 가상 머신은 가비지 컬렉터(garbage collector)를 이용하여 더는 사용하지 않는 메모리를 자동으로 회수해 줍니다. 따라서 개발자가 따로 메모리를 관리하지 않아도 되므로, 더욱 손쉽게 프로그래밍을 할 수 있도록 도와줍니다.


# JVM의 구조
<img src="https://3553248446-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M5HOStxvx-Jr0fqZhyW%2F-MG6-n2RCnRrss4KBsSz%2F-MG7f7yiI__p7MZ5dcR4%2Fimage.png?alt=media&token=67393c91-2a56-4277-8a88-f2e606f80969" alt="JVM 구성 요소" width="500px">   

### Class Loader
.class(byte code)들을 실제 메모리에 적재하는 역할을 합니다.   
자바에서 소스를 작성하면 .java파일이 생성되고 .java소스를 컴파일러가 컴파일하면 .class파일이 생성되는데 클래스 로더는 .class 파일을 묶어서 JVM이 운영체제로부터 할당받은 메모리 영역인 Runtime Data Area로 적재합니다.

### Execution Engine
Execution Engine(실행엔진)은 JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행한다.   
클래스 로더에 의해 JVM으로 로드된 .class 파일(바이트코드)들은 Runtime Data Areas의 Method Area에 배치되는데, 배치된 이후에 JVM은 Method Area의 바이트 코드를 실행 엔진(Execution Engine)에 제공하여, 정의된 내용대로 바이트 코드를 실행시킵니다. 이때, 로드된 바이트코드를 실행하는 런타임 모듈이 실행 엔진(Execution Engine)입니다. 실행 엔진은 바이트코드를 명령어 단위로 읽어서 실행합니다.

### Runtime Data Area
JVM이 자바 바이트코드를 실행할 때 여러 종류의 메모리 공간이 필요한데, 이때 사용되는게 Runtime Data Area 입니다.   
영역들을 스레드 공유 유무에 따라 분류하면 다음과 같습니다.

1. 모든 스레드가 공유
 - Method(Class, Static) Area
    - Method Area는 클래스 로더가 클래스 파일을 읽어오면, 클래스 정보를 파싱해서 저장하는 곳
    - 멤버(클래스, 인스턴스)변수와 상수(final), 클래스와 메소드, 데이터 타입,  정보 등이 저장되는 공간

 - Heap Area
    - 프로그램을 실행하면서 생성한 모든 객체를 저장하는 공간
    - new 키워드로 생성된 객체와 배열 등의 참조형 변수정보가 저장되는 공간
    - Method Area에 올라온 클래스들만 생성 가능
    - jdk 8 이상 : static 변수, string 상수 풀
    - GC의 대상

2. 스레드마다 존재
- PC(Program Counter)
  - 각 스레드는 메서드를 실행하고 있고, pc는 그 메서드안에서 몇번째 줄을 실행해야 하는지 나타내는 역할을 한다.
  - 쓰레드마다 하나씩 생성. 
  - JVM 명령의 주소값이 저장되는 공간
- Stack Area
  - 자바 스택은 스레드 별로 1개만 존재한다.
  - 스택 프레임은 메서드가 호출될 때마다 생성된다.(push) 
  - 메서드 실행이 끝나면 pop되어 스택에서 제거된다.
  - 클래스 내의 메소드에서 사용되는 정보들이 저장되는 공간 
  - 매개변수, 지역변수, 리턴값 등이 저장되며 LIFO(Last In First Out) 방식으로 메소드 실행 시 저장되었다가 실행이 완료되면 제거된다. 임시저장

- Native Method Stack Area
  - 성능향상을 목적으로 자바 바이트코드가 아닌 다른 언어로 작성된 네이티브 메서드((C/C++)를 위한 메모리 영역


### garbage collector
 **Heap 메모리 영역**에 생성(적재)된 객체들 중에 참조되지 않은 객체들을 탐색 후 제거하는 역할을 하며 해당 역할을 하는 시간은 정확히 언제인지를 알 수 없습니다. GC역할을 수행하는 스레드를 제외한 나머지 모든 스레드들은 일시정지상태가 됩니다.


---
### 참고
자바의정석   
https://coding-factory.tistory.com/828
https://coding-factory.tistory.com/827