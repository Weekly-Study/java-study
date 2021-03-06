# 컴퓨터 언어와 사람이 쓰는 언어

컴퓨터는 사람이 ‘가', ‘나', ‘다'를 쓰는 것과는 다르게 ‘0’과 ‘1’로만 명령을 이해하고 실행한다.

이 차이점으로 컴퓨터가 쓰는 언어와 사람이 쓰는 언어를

기계 중심 언어인 `저급언어`, 사용자 중심 언어인 `고급언어`라고 부른다.

## 컴파일과 링크

사용자가 고급 언어로 프로그래밍을 하면 기계가 이해할 수 있도록 기계어로 번역하는 과정이 필요한데, 

이를 `컴파일` 이라고 한다.

사용자가 이해하는 언어로 작성된 코드를 원시코드,기계가 이해하는 언어로 번역한 것을 목적코드(목적파일) 라고 한다.

따라서 컴파일을 원시코드를 목적코드로 번역하는 것이라고도 표현할 수 있다.

컴파일 한 목적 파일을 실행 파일로 바꾸는 것을 `링크`라고 말하는데,

컴파일과 링크를 수행하는 것을 `컴파일러`라고 한다.

# JVM

`Java Virtual Machine`

프로그래밍 언어 중 Java로 작성된 프로그램이 플랫폼(운영체제)에 구애받지 않고 독립적으로 동작할 수 있도록 해주는 역할을 한다.

자바 바이트 코드를 해당 운영체제에 맞는 기계어로 재번역한 후 실행함으로써 운영체제와 자바 프로그램을 연결시켜주는 역할을 한다.

<img width="711" alt="JAVA와 JVM" src="https://user-images.githubusercontent.com/47437757/167302129-9333cc03-18bd-4e91-8219-7e06027c18d7.png">

# Java의 컴파일 및 실행 과정

Java의 컴파일 및 실행 과정은 크게 4단계로 나누어 볼 수 있다.

<img width="831" alt="Java_code_컴파일실행과정" src="https://user-images.githubusercontent.com/47437757/167302120-a8f2d3b4-5370-4082-aac2-3c022a06def6.png">

1. Java 언어로 작성된 소스 코드를 JVM이 이해할 수 있는 자바 바이트 코드 파일로 컴파일 한다.
2. 컴파일된 코드를 자바의 Class Loader에게 전달한다.
3. 클래스 로더가 코드들을 로딩 및 링크해서 JVM 메모리에 올린다.
4. 실행엔진(Execution Engine)이 JVM 메모리에 올라 온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행한다.

## 1. 자바 컴파일러

자바 소스 코드 .java 파일을 실행하기 위해서는 자바 컴파일러가 소스 코드를 `바이트 코드인 .class 파일`로 번역해줘야 한다.

### 자바 바이트 코드

자바 소스 코드르 JVM이 이해할 수 있는 언어로 변환한 코드를 의미한다.

자바 컴파일러에 의해 변환되는 코드의 명령어 크기가 `1바이트`이기 때문에 자바 바이트 코드라고 불리운다.

확장자는 `.class`이다.

자바 바이트 코드는 JVM만 있다면 어떤 운영체제에서든지 실행할 수 있다.

## 2. 클래스 로더

클래스 로더는 JVM이 종료될 때까지 `동적 로딩` 방식을 이용해서 

자바 컴파일러가 변역해 둔 클래스(.class 파일)들을 찾아와서 JVM의 메모리(Runtime Data Area)에 올려주는 역할을 한다.

### 클래스 로더의 동적 로딩

![Runtime Data Area](https://user-images.githubusercontent.com/47437757/167302307-3b1fda80-dca9-4b8f-8782-ee01a7ce53c6.png)

런타임 중 어떤 메소드를 호출하는 문장을 만났는데, 

그 메소드를 가진 바이트 코드가 아직 로딩된 적이 없다면 JVM이 클래스를 동적으로 찾기 시작한다.

- 로드
    
    JRE 라이브러리 폴더 > CLASSPATH 환경변수에 지정된 폴더 
    
    순으로 해당 폴더를 찾아가 `클래스 파일을 찾아 온 후 JVM 메모리에 로드한다.`
    
- 검증
    
    찾고 나면 로딩하기 전, 올바른 바이트 코드인지 `검증` 과정을 거친다.
    
    자바 언어 명세(Java Language Specification) 및 JVM 명세에 명시된 대로 구성되어 있는지 검사한다.
    
    올바른 바이트 코드라면 `Method 영역으로 파일을 로딩`한다.
    
- 준비
    
    필드, 메서드, 인터페이스 등 클래스가 필요로 하는 메모리를 할당한다. 
    
    클래스 변수를 만들라는 명령어가 있으면 `Method 영역에 변수를 준비`한다.
    
- 분석
    
    클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경한다.
    
- 초기화
    
    클래스 변수들은 적절한 값으로 초기화 한다.
    

위와 같은 과정이 클래스 로더가 동적으로 바이트 코드를 로딩하는 과정이다.

## 3. 실행 엔진

실행 엔진(Execution Engine)은 JVM 메모리에 적재된 클래스들을 기계어로 번역해 명령어 단위로 실행하는 역할을 한다.

실행 방식엔 인터프리터 방식과 JIT 방식 두 가지가 있다.

### 자바와 순수 컴파일러와의 차이

![JIT컴파일러](https://user-images.githubusercontent.com/47437757/167302131-d378ef0c-300e-4ee3-b3f5-ad12cbe0cf8a.png)

자바는 소스 코드 변환에 있어서 

컴파일 시점에 바이트 코드로 한 번 `컴파일` 하는 과정과,

런타임 시점에 바이트 코드를 바이너리 코드로 `인터프리터` 하는 방식 2단계를 거친다.

때문에, 순수 컴파일러만 수행하는 C언어 등에 비해 컴파일 방식이 느리다는 평가가 있다.

### 인터프리터

바이트 코드 명령어를 하나 하나씩 읽어들여서 실행하는 방식이다.

하나하나의 실행은 빠르지만 전체적인 실행 속도는 느리다.

중복되는 코드가 있다 해도 라인별로 실행하는 방식이기 때문에 같은 내용을 다시 인터프리팅 하는 과정이 들어간다.

런타임 전 소스코드를 미리 읽어서 기계어로 변환하는 방식의 순수 컴파일러보다 느릴 수 밖에 없다.

### JIT 컴파일러

번역해 둔 코드를 캐싱해 둔 다음 똑같은 코드가 있다면 번역하지 않고 캐싱해 둔 값을 사용하는 방식이다. 

인터프리터 방식을 보완하기 위해 나온 방법으로, 

인터프리터와 컴파일러의 방식을 혼합해서 속도를 개선한 방식이다.

`Just-In-Time Compiler`

JIT는 Just In Time의 약자로 `‘제 때’` 컴파일 한다는 의미로 사용한다.

여기서 이 ‘제 때’의 의미는 처음 호출될 때 의미가 아니라는 것을 알아야 한다.

 JIT 컴파일 방식에서 메서드는 처음 호출되자마자 컴파일 되지 않는다. 

JVM은 호출되는 메서드 각각마다 호출 횟수를 누적하고 그 횟수가 특정 수치를 초과할 때 컴파일을 한다.

이 때, 컴파일 시점을 판단하는 수치 기준을 `컴파일 임계치`라고 한다.

# JVM의 구성요소

JVM은 크게 `Class Loader`, `GC`, `Runtime Data Area`, `Execution Engine` 네 가지로 나뉜다.

![JVM](https://user-images.githubusercontent.com/47437757/167302132-bf997057-8190-4c33-8b64-a636fb2340a9.png)

![JVM상세구조](https://user-images.githubusercontent.com/47437757/167302304-4cdb2932-69ae-4d5e-bfda-7101bcf8ad37.png)

## Garbage Colletor

Heap 메모리 영역에 생성된 객체들 중에  유효한 주소를 잃어버려서 사용할 수 없는 객체(Reachability를 잃은 객체)를 탐색 후 제거하는 역할을 한다.

## Runtime Data Area

- **Method Area**
    
    클래스 멤버 변수, 메서드 정보, Type(Class or Interface) 정보, Constant Pool, static, final 변수 등이 생성되는 영역이다.
    
    상수 풀은 모든 Symbolic Reference를 포함하고 있다.
    
- **Heap Area**
    
    동적으로 생성된 오브젝트오 배일이 저장되는 곳으로 GC의 대상이 되는 영역이다.
    
- **Stack Area**
    
    지역 변수, 파라미터 등이 생성되는 영역이다.
    
    동적으로 객체를 생성하면 실제 객체는 Heap에 할당되고 해당 레퍼런스만 Stack에 저장된다.
    
    Stack은 스레드별로 독자적으로 가진다.
    
    Heap에 있는 객체가 Stack에서 참조할 수 없는 경우(주소값을 잃은 경우) GC의 대상이 된다.
    
- **PC Register**
    
    현재 스레드가 실행되는 부분의 주소와 명령을 저장하고 있다. (CPU의 PC Register와 다른 것이다.)
    
- **Native Method Stack**
    
    자바외 언어로 작성된 네이티브 코드를 위한 메모리 영역이다.
    

# JDK와 JRE의 차이

## JRE

`Java Runtime Environment`

컴파일된 Java 프로그램을 실행하는데 필요한 패키지이다.

자바 가상 머신, 자바 클래스 라이브러리, 자바 명령 및 기타 인프라를 포함하고 있다.

### JRE 포함 폴더

- `bin/`

Java 실행 프로그램이 포함되어 있다.

JVM을 시작하는 java (Window라면 javaw)가 포함되어 있다.

또한 keytool 및 policytool과 같은 다른 유틸리티도 있다.

- `conf/`

사용자가 편집할 수 있는 구성 파일 (configuration files)가 있다.

- `lib/`

여러가지 supporting 파일이 있다.

jar 구성 파일, 속성 파일, 글꼴, 번역, 인증서 등 java의 모든 trimming들이 있다.

가장 중요한 것은 모듈인데, Java 표준 라이브러리의 .class파일을 포함하는 모듈이 있다.

- 네이티브 코드를 호출하기 위해, 시스템 별 네이티브 바이너리 코드를 지원하는 .dill(Window), dylib(macOS), .so(Linux) 파일이 `bin/` 또는 `lib/` 아래에 포함되어 있다.

## JDK

Java Development Kit

Java를 사용하기 위해 필요한 모든 기능을 갖춘 Java용 SDK(Softwage Development Kit)이다.

JRE에 있는 모든 것 뿐만 아니라 컴파일러(javac)와 jdb, javadoc과 같은 도구도 있다.

이를 통해 JDK는 프로그램을 생성하고 컴파일할 수 있다.

![JVM과 JRE](https://user-images.githubusercontent.com/47437757/167302164-c3bd8b3f-1ea2-4dc4-96e4-d4ea534ecc80.png)

JDK는 JRE를 포함하고 있다.

컴퓨터에서 Java 프로그래밍을 실행하는데에 초점을 맞춘다면 JRE만 설치하면 되고

Java 프로그래밍을 하는데에 초점을 맞춘다면 JDK를 설치해야 한다.

Java 프로그래밍을 하지 않더라도 JDK를 설치해야 하는 경우도 있다.

JSP를 사용한다면 WAS가 JSP를 자바 서블릿으로 변환하고 JDK를 사용하여 서블릿을 컴파일 해야 하기 때문이다.

> 출처
[1] [https://beststar-1.tistory.com/3](https://beststar-1.tistory.com/3)  
[2] [https://coding-nyan.tistory.com/85](https://coding-nyan.tistory.com/85)  
[3] [https://velog.io/@woo00oo/자바-컴파일-과정](https://velog.io/@woo00oo/%EC%9E%90%EB%B0%94-%EC%BB%B4%ED%8C%8C%EC%9D%BC-%EA%B3%BC%EC%A0%95)  
[4] [https://velog.io/@litien/JVM-구조](https://velog.io/@litien/JVM-%EA%B5%AC%EC%A1%B0)  
[5] [http://www.tcpschool.com/java/java_intro_programming](http://www.tcpschool.com/java/java_intro_programming)  
[6] [https://developerntraveler.tistory.com/49](https://developerntraveler.tistory.com/49)  
>
