# 자료형

우리가 사용하는 값(data)의 종류는 크게 문자와 숫자로 나눌 수 있다.

숫자는 다시 정수와 실수로 나눌 수 있다.

이러한 값의 종류에 따라 값이 저장될 공간의 크기와 저장형식을 정의한 것이 자료형 data type이다.

## 기본형과 참조형

자료형은 기본형과 참조형 두 가지로 나눌 수 있다.

- 기본형 primitive type
    - 변수에 실제 값을 저장할 수 있게 한다.
- 참조형 reference type
    - 변수에 어떤 값이 저장되어 있는 주소 (memory address)를 저장할 수 있게 한다. (객체의 주소를 저장한다.)
    - 기본형(원시타입)을 제외한 대부분의 자료형은 참조형이라고 보면 된다.

JAVA는 참조형 변수 간 연산을 할 수 없어, 참조형 변수를 사용하더라도 연산에 사용되는 값은 모두 기본형 변수이다.

### 기본형

| 기본형 | 논리형 | boolean | 1byte (8bit) | 조건식과 논리적 계산에 사용 |
| --- | --- | --- | --- | --- |
|  | 문자형 | char | 2byte (16bit) | 변수에 하나의 문자만 저장할 수 있다. |
|  | 정수형 | byte | 1byte (8bit) | byte는 이진 데이터를 다룰 때 사용. |
|  |  | short | 2byte (16bit) | short는 C언어와의 호환을 위해 추가. |
|  |  | int | 4byte (32bit) |  |
|  |  | long | 8byte (64bit) |  |
|  | 실수형 | float | 4byte (32bit) | 실수를 저장할 때 사용. |
|  |  | double | 8byte (64bit) | 실수를 저장할 때 사용. |

문자형인 char는 문자를 내부적으로 정수(유니코드)로 저장하기 때문에 정수형과 별반 다르지 않다고도 볼 수 있다.

boolean을 제외한 나머지 7개의 기본형끼리는 서로 연산과 변환이 가능하다.

### 기본형 값의 범위

| boolean |  | false, true |
| --- | --- | --- |
| char |  |  |
| byte | ⁍ |  |
| short |  |  |
| int |  |  |
| long |  |  |
| float |  |  |
| double |  |  |

# Literal과 Constant Pool

데이터 자체를 의미한다.

변수에 넣는 변하지 않는 데이터(값)를 말한다.

자료형 중 기본형과 String이 리터럴에 해당한다.

```java
int a = 1;
int b = 1;
```

위의 코드에서 a와 b는 변수이고, 1이 리터럴이다.

![literal_primitive_type](https://user-images.githubusercontent.com/47437757/168476798-c682a9ec-6b69-4c39-9c1b-716e39826e1f.png)

![literal_string_type](https://user-images.githubusercontent.com/47437757/168476803-be34867e-050e-4b3b-b6c6-a3e9a2057195.png)

Heap 메모리 영역 안에 있는 Constant Pool이라는 영역에 데이터를 할당하고

같은 값을 여러 변수에서 사용한다면, 메모리 낭비를 막기 위해 해당 값이 할당되어 있는 메모리 주소를 넘겨서 사용하게 한다.

String 타입의 경우 String Contant Pool이라는 별도의 영역에서 데이터를 처리하다.

## 리터럴과 프로그래밍에서의 상수

<aside>
💡 Literal은 수학에서의 상수와 같다.  
하지만, 프로그래밍에선 상수를 ‘값을 한 번 저장하면 변경할 수 없는 저장공간'으로 정의했기 때문에  
프로그래밍의 상수와 구분하기 위해서 Literal이란 이름으로 정의했다.

</aside>

### 상수 Constant

상수의 정의는 아래와 같다.

- 값을 저장할 수 있는 공간 (변수의 정의)
- 한 번 값을 저장하면 다른 값으로 변경할 수 없는 공간

```java
final int MAX_COUNT = 7;
```

변수 앞에 final 키워드를 붙이면 상수가 된다.

상수는 반드시 선언과 동시에 초기화해야 하며, 선언한 후 그 값을 변경할 수 없다.

상수의 명은 모두 대문자로 하며, 여러 단어를 결합해서 지을 경우 ‘_’로 구분하는 것이 규칙이다.

### 상수의 의미

# 변수

자바에서 값을 사용하기 위해서는 메모리 영역의 일정 공간에 값을 저장해둬야 한다.

이를 변수를 선언한다라고 표현한다.

미리 자원을 확보해두고 사용하는 것이다.

```java
boolean pass;

int a, b;//다중 변수 선언
```

변수 선언은 사용할 데이터에 맞는 자료형을 명시하고, 변수의 이름을 명명해주면 된다.

```java
boolean pass = false;
```

변수를 선언한 후 사용하기 위해서는 값을 할당해야 한다. 이를 초기화한다고 한다.

변수 선언과 초기화는 같이 할 수도, 따로 할 수도 있다.

## 변수의 Scope와 Life time

변수를 선언할 때엔 변수에 접근할 수 있는 영역에 대해서도 이해하고 있어야 한다.

기본적인 규칙으로는 변수를 선언한 블록내에서만 접근 가능하는 것이 있다.

블록은 { } 중괄호로 구분한다.

자바에서 변수는 scope에 따라 클래스 변수, 인스턴스 변수, 지역 변수로 나눌 수 있다.

우선 클래스 내부에 선언되어 있는 변수는 멤버 변수라고 표현한다.

|  | 정의 | scope | life time |
| --- | --- | --- | --- |
| 클래스 변수
Class Variable

(또는
전역 변수
Global Variable) | 클래스 내부이면서 모든 블록 외부에서 선언되어 있고, static으로 표시된 변수 | 클래스 전체
(클래스 내 모든 장소에서 사용할 수 있기 때문에 
전역 변수라고도 부르는 것) | 클래스가 메모리에 로드되어 있는 동안
또는, 프로그램이 끝날 때까지 유지 |
| 인스턴스 변수
Instance Variable | 클래스 내부이면서 모든 메서드 및 블록 외부에서 선언된 변수 | 정적(static) 메서드를 제외한 클래스 전체 | 객체가 메모리에 남아있는 동안 유지 |
| 지역 변수
Local Variable | 인스턴스 및 클래스 변수가 아닌 모든 변수
(메서드 내에서 선언한 변수) | 선언된 블록 내 | 런타임시 해당 변수가 선언되어 있는 블록에 들어와서 그 블록을 벗어나기 전까지 유지 |

```java
public class Product {

	private static String type = "fruit";// 클래스 변수
	private String name;// 인스턴스 변수

	pulic boolean isBeForSale(int stock) {// 지역 변수
		return stock > 0 ? true : false;
	}
}
```

# 형 변환 Data Type Conversion

- 캐스팅은 데이터 손실을 막는 것에 방점을 두고 있다.
- 캐스팅은 서로 관련 있는 자료형 사이에서 이루어진다.

## 기본형의 Casting

기본형의 형 변환은 자동 타입 변환과 강제 타입 변환 2가지로 분류한다.

보다 큰 크기의 데이터와 보다 작은 크기의 데이터 간 어느 쪽으로 형 변환을 하느냐에 따라 자동 타입 변환이 적용되거나 강제 타입 변환이 필요하다.

- 자동 타입 변환
    - 개발자가 지정하지 않아도 자동으로 이루어지는 타입 변환
- 강제 타입 변환
    - 개발자가 명시해야만 이루어지는 타입 변환

### 자동 타입 변환

작은 크기의 데이터에서 큰 크기의 데이터로 변환할 경우,

원본 데이터의 손실없이 그대로 보존할 수 있기 때문에 자동 타입 변환이 일어난다.

`byte → short → int → long`

자동 타입 변환을 `프로모션` 이라고도 한다.

### 강제 타입 변환

큰 크기의 데이터에서 작은 크기의 데이터로 변환할 경우,

원본 데이터가 그대로 보존될 수도, 손실될 수도 있기 때문에 자동 타입 변환이 일어나지 않는다.

원본 데이터 손실을 감수하고 형변환을 하고 싶을 경우 개발자가 명시적으로 타입 변환을 지정해주는 것을 강제 타입 변환이라고 한다.
(OOP의 다형성을 이용하고자 하는 경우라면 강제 형 변환이 필요할 수 있다.)

명시적으로 형 변환을 해주지 않으면 컴파일 에러가 발생한다.

- 예시

```java
int a = 1; //4byte
short b = (short) a; //2byte
```

변환하고자 하는 작은 크기의 타입을 ( ) 괄호 안에 지정해주면 된다.

- 원본 데이터 손실 예

```java
double a = 1.7;
int b = (int) a; // b는 1
```

위의 코드에서 변수 a 1.7은 int형으로 변환하면서 소수점 아래가 버려지고 1로 변환된다.

```java
double a = 1;
```

<aside>
💡 위의 코드의 경우 컴파일 에러가 발생하지 않고 자동 형 변환이 되는데,  
컴파일러가 이미 알고 있는 기본형 자료들이기 때문에 자동으로 (double)을 넣어 캐스팅을 해준 것이다.

이와 달리 참조형 데이터는 컴파일러가 추리해낼 수 있는 타입이 아니기 때문에 컴파일러가 자동으로 캐스팅을 수행할 수 없다.

</aside>

## 참조형의 Casting

참조형은 컴파일러가 사전에 알고 있는 자료형이 아니기 때문에 기본형 캐스팅과는 차이가 있다.

참조형 캐스팅을 하기 위해선 각 참조형 간에 아래 정보를 파악해야 한다.

1. 상속관계에 있는지
2. 인터페이스로 인해 확장되었는지

참조형은 위 두가지 정보로 업캐스팅과 다운캐스팅을 할 수 있다.

### 업캐스팅

상속 관계인 Parent 클래스와 Child 클래스가 있을 경우

Child 클래스는 Parent 클래스가 가진 데이터와 같은 데이터를 가지고 있거나 그 이상의 데이터를 가지고 있을 것이다.

```java
Parent parent = (Parent) new Child();
```

이런 경우 Parent에 필요한 값들을 Child가 모두 가지고 있기 때문에 Child의 인스턴스를 Parent로 형변환하는 것이 가능하다.

이렇게 상속관계인 자식 객체를 부모 객체로 변환하는 것을 업캐스팅이라고 한다.

이때 (Parent) 캐스팅은 생략이 가능하다. 컴파일러가 추론이 가능하기 때문이다.

### 다운캐스팅

반면에, 아래처럼 부모 객체를 자식 객체로 형변환하는 다운캐스팅은 불가능하다.

```java
Child child = new Parent();
```

Parent는 Child에 필요한 정보를 모두 충족시키지 않기 때문이다.

```java
Child child = (Child) new Parent();
```

직접 형변환을 해줄 경우 컴파일 오류는 피할 수 있지만, 런타임에서 오류가 발생한다.

```java
Parent parent = new Child();
Child child = (Child) parent;
```

다만, 위와 같이 업캐스팅이 선행됐을 경우 Child에 필요한 정보를 모두 갖추고 있기 때문에 다운캐스팅을 할 수 있다.

# 1차 배열과 2차 배열 선언하기

같은 타입의 여러 변수를 하나의 묶음으로 다루는 것을 배열 Array이라고 한다.

아래와 같이 선언과 초기화를 할 수 있다.

```java
String[] fruit; // 타입[] 변수이름; or 타입 변수이름[];
fruit = new String[5];// 초기화
```

2차원 배열은 아래와 같이 선언할 수 있다.

```java
int[][] score = new int[4][3];
```

# 타입 추론 Local-Variable Type Inference

컴파일러가 데이터(값)을 보고 자료형을 추론해내는 것을 타입 추론이라고 한다.

Java 10부터 변수를 선언할 때 타입을 생략하고 var로 표현할 수 있게 되었다.

지역 변수에만 사용할 수 있다.

```java
var a = 10;
var b = "name"
```

위의 경우, 컴파일러가 10과 “name”이라는 값을 보고 자료형을 추론할 수 있기 때문에 var 타입을 쓰더라도 컴파일 에러가 발생하지 않는다.

- 초기화를 안하거나
- null값으로 초기화를 하거나
- 배열에 타입 추론을 사용하려 하거나
- lambda에 타입 추론을 사용하려 하거나

위 내용들은 컴파일러가 타입을 추론해낼 수 없기 때문에 컴파일 에러가 발생한다.

출처  
[1] 자바의 정석  
[2] [https://yoo11052.tistory.com/50](https://yoo11052.tistory.com/50)  
[3] [https://www.devkuma.com/docs/java/literal/](https://www.devkuma.com/docs/java/literal/)  
[4] [https://7942yongdae.tistory.com/22](https://7942yongdae.tistory.com/22)  
[5] [https://itmining.tistory.com/20](https://itmining.tistory.com/20)  
[6] [https://wakestand.tistory.com/179](https://wakestand.tistory.com/179)  
[7] [https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=kimkwon429&logNo=220742301090](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=kimkwon429&logNo=220742301090)  
[8] [https://mommoo.tistory.com/41](https://mommoo.tistory.com/41)  
[9] [https://codechacha.com/ko/java-local-variable-type-inference/](https://codechacha.com/ko/java-local-variable-type-inference/)
