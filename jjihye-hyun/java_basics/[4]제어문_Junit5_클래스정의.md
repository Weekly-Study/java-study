# 제어문(Control Statement)
프로그램의 흐름을 바꾸는 문장들을 제어문이라고 한다. 제어문에는 조건문과 반복문이 있는데, 조건문은 조건에 따라 다른 문장이 수행되도록 하고, 반복문은 특정 문장들을 반복해서 수행한다.

## 선택문
### if문
if문은 '조건식'과 '괄호{}'로 이루어져 있다. 만일(if) 조건식이 참(true)이면 괄호{} 안의 문장들을 수행하라 라는 의미로 해석된다. 만일 조건식의 결과가 false이면 괄호{}안의 문장은 수행되지 않는다. 조건식은 일반적으로 비교연산자와 논리연산자로 구성된다.

```java
if(조건식) {
    // 조건식이 참(true)일 때 수행될 문장들을 적는다.
}
```
### if-else문
조건식의 결과가 참이 아닐 때, 즉 false일 때 else블럭의 문장을 수행하라는 의미이다.

```java
if(조건식) {
    // 조건식이 참(true)일 때 수행될 문장들을 적는다.
} else {
    // 조건식이 거짓(false)일 때 수행될 문장들을 적는다.
}
```
### if-else if문
여러개의 조건식을 써야하는 경우 사용한다.

```java
if(조건식1) {
    // 조건식1이 참(true)일 때 수행될 문장들을 적는다.
} else if(조건식2) {
    // 조건식2이 참(true)일 때 수행될 문장들을 적는다.
} else if(조건식3) { // 여러개의 else if를 사용할 수 있다.
    // 조건식3이 참(true)일 때 수행될 문장들을 적는다.
} else { // 마지막에는 보통 else블럭으로 끝나며, else블럭은 생략 가능하다.
    // 위의 어느 조건식도 만족하지 않을 때 수행될 문장들을 적는다.
}
```
### switch문
하나의 조건식으로 많은 경우의 수를 처리할 수 있다.   

1. 조건식을 셰산한다.
2. 조선식의 결과와 일치하는 case 문으로 이동한다.
3. 이동한 case문 아래에 있는 문장들을 수행한다.
4. break이나 switch문의 끝을 만나면 switch문 전체를 빠져나온다. 

```java
switch(조건식){
    case 값1:
        // 조건식의 결과가 값1과 같을 경우 수행될 문장들
        break; // switch 문을 벗어난다.
    case 값2:
        // 조건식의 결과가 값2과 같을 경우 수행될 문장들
        break; // switch 문을 벗어난다.
    default:
        // 조건식의 결과와 일치하는 case문이 없을 때 수행될 문장들
}
```
- break 문은 각 case문의 영역을 구분하는 역할을 한다. 만약 break문이 없다면 다른 break문을 만나거나 switch문 블랙의 끝을 만날 때까지 나오는 모든 문장들을 수행한다.
- case문의 값은 정수 또는 문자열, 상수만 가능하며 중복되지 않아야 한다.
- switch 조건식의 결과는 정수 또는 문자열이어야 한다.

## 반복문
반복문은 어떤 작업이 반복적으로 수행되도록 할 때 사용한다.

### for문
주로 반복 횟수를 알고 있을 때 사용한다.
```java
for(초기화; 조건식; 증감식){
    // 조건식이 참일 때 수행될 문장들을 적는다.
}

for(int i=1; i<=5; i++){
    System.out.println("I can do it!");
}

```
- 초기화: 반복문에 사용될 변수를 초기화하는 부분이며 처음에 한번만 수행된다. 둘 이상의 변수가 필요할 때는 콤마로 구분. 단, 두 변수의 타입은 같아야 함
- 조건식: 조건식의 값이 참이면 반복하고 거짓이면 반복을 준단하고 for문을 벗어난다.
- 증감식: 반복문을 제어하는 변수의 값을 증가 또는 감소시키는 식이다. 매 반복마다 변수의 값이 증감식에 의해서 점진적으로 변하다가 결국 조건식이 거짓이 되어 for문을 벗어나게 된다.

### 향상된 for문
배열이나 컬렉션에 저장된 요소들을 읽어오는 용도로 사용.

```java
for(타입 변수명: 배역 또는 컬렉션){
    // 반복할 문장
}
for(int tmp: arr){
    System.out.println(tmp);
}


```

### while문
while문은 조건식이 참인 동안, 즉 조건식이 거짓이 될때 까지 블랙{}내의 문장을 반복한다. 

```java
while(조건식){
    // 조건식이 참일 때 반복될 문장들을 적는다.
}
```
```java
// for 문과 while문 비교

for(int i = 1; i<=10; i++){
    System.out.println(i);
}

int i = 1;
while(i<=10){
    System.out.println(i);
    i++;
}

```

### do-while문
while문은 조건식의 결과에 따라 블럭{}이 한번도 수행되지 않을 수 있지만, do-while은 최소한 한번은 수행될 것을 보장한다.

```java
do {
    // 조건식이 참일 때 반복될 문장들을 적는다.
} while(조건식);    // ; 주의
```

### break문
break문은 자신이 포한된 가장 가까운 반복문을 벗어난다. 주로 if 문과 함께 사용되어 특정 조건을 만족하면 반복문을 벗어나도록 한다.
```java
int sum = 0;
int i = 0;

while(true){
    if( sum > 100)
        break;
    i++;
    sum += i;
}
```

### continue문
continue문은 반복문 내에서만 사용될 수 있으며, 반복이 진행되는 도중에 continue문을 만나면 반복문의 끝으로 이동하여 다음 반복으로 넘어간다. for문의 경우 증감식으로 이동하고, while문의 경우 조건식으로 이동한다. 주로 if 문과 함께 사용되어 특정 조건을 만족하는 경우 continue문 이후의 문장들을 수행하지 않고 다음 반복으로 넘어가서 계속 진행하도록 한다. continue문은 반복문 전체를 벗어나지 않고 다음 반복을 계속 수행한다는 점이 break문과 다르다.
```java
for(int i= 0; i<=10; i++){
    if(i%3==0)
        continue;
    System.out.println(i);
}

```

---

# JUnit5
JUnit5는 자바 테스팅 프레임워크이다.

```java
// JUnit5의 세부 모듈

[Jupiter][Vintage]
[ Junit Platform ]
```
- Platform: 테스트를 실행해주는 런처 제공. TestEngine API 제공.
- Jupiter: Junit5 TestEngine API 구현체
- Vintage: Junit4, Junit3 지원하는 TestEngine 구현체

## Junit5 시작하기
- Springboot2.2 이상에서는 spring-boot-starter-test에서 junut5제공
- 그 외, maven dependency 추가
```java
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.5.2</version>
    <scope>test</scope>
</dependency>
```
```java
@Test
void create_new_study(){
    Study study = new Study();
    assertNotNull(study);
}
```
- @Test
- @BeforeAll: 모든 테스트들 실행하기 전에 딱 한번 실행됨, 반드시 static void 메서드로 작성
- @AfterAll: 모든 테스트들 실행 후에 딱 한번 실행됨, 반드시 static void 메서드로 작성
- @BeforeEach: 테스트 실행하기 전에 각각 실행
- @AfterEach: 테스트 실행 후에 각각 실행
- @Disabled: 테스트 실행하지 않음


## Junit5 테스트 이름 표시하기
- <code>@DisplayNameGeneration</code>: Method와 Class 레퍼런스를 사용해서 테스트 이름을 표기하는 방법 설정.
기본 구현체로 ReplaceUnderscores 제공
- <code>@DisplayName</code>: 어떤 테스트인지 테스트 이름을 보다 쉽게 표현할 수 있는 방법을 제공하는 애노테이션. @DisplayNameGeneration 보다 우선 순위가 높다.

```java
class StudyTest {

    @Test
    @DisplayName("스터디 만들기")
    void create_new_study(){
        Study study = new Study();
        assertNotNull(study);
    }
}

```

## Junit5 Assertion
org.junit.jupiter.api.Assertions.*
|    |     |
| --- | --- |
| assertEqulas(expected, actual) | 실제 값이 기대한 값과 같은지 확인|
| assertNotNull(actual) | 값이 null이 아닌지 확인 |
| assertTrue(boolean) | 다음 조건이 참(true)인지 확인 |
| assertAll(executables...) | 모든 확인 구문 확인 |
| assertThrows(expectedType, executable) | 예외 발생 확인 |
| assertTimeout(duration, executable) | 특정 시간 안에 실행이 완료되는지 확인 |

---
# 클래스	
클래스란 객체를 정의해 놓은 것 또는 객체의 설계도 또는 틀이라고 정의할 수 있다. 클래스는 객체를 생성하는데 사용되며, 객체는 클래스에 정의된 대로 생성된다.   
프로그래밍에서의 객체는 클래스에 정의된 내용대로 메모리에 생성된 것을 뜻한다.

## 클래스 정의하는 방법
클래스에는 객체의 모든 속성과 기능의 정의되어 있어, 클래스로부터 객체가 생성되면 클래스에 정의된 속성과 기능을 가진 객체가 만들어지는 것이다.
- 속성(property): 멤버변수, attribute, 필드, 상태
- 기능(function): 메서드(methed), 함수, 행위

```java

접근지정자 class 클래스이름 {
    // 멤버 변수
    // 생성자
    // 메소드
}

```
```java

class Car {
    String color;

    Car(){}

    Car(String c){
        color = c;
    }
}

```

---
### 참고
- 도서, 자바의 정석
- 더 자바, "코드를 테스트 하는 다양한 방법