# Enum

`열거형`이라고도 한다.

<aside>
💡 서로 연관된 상수들의 집합이 Enum이다.

</aside>

Enum은 Interface, class와 동급으 형식을 가지는데, 사실상 class라고 볼 수 있다.

Enum만을 위한 문법적 형식을 가지고 있기 때문에 구분하기 위해서 Enum이라고 분류를 해둔 것이다.

장점으로는 아래와 같은 내용이 있다.

- 상수들의 값뿐만 아니라 타입까지 관리할 수 있어, 타입에 안전하게 사용할 수 있다.
- 상수의 값이 바뀌어도 다시 컴파일할 필요가 없다.

## 정의하기

가장 단순하게 enum을 정의하는 방법은 아래와 같다.

```java
enum Type {
	NORTH,
	EAST,
	SOUTH,
	WEST
}
```

열거형의 이름을 정의하고, 열거형이 가질 `상수`명만을 정의한 형태이다.

열거형의 상수에 `속성`을 부여할 수도 있다. 속성은 하나 이상 부여할 수 있다.

```java
public enum Type {
    NORTH("북쪽"),
    EAST("동쪽"),
    SOUTH("남쪽"),
    WEST("쪽");

    private final String korean;

    Type(String korean) {
        this.korean = korean;
    }
}
```

이렇게 속성을 부여해두고, 해당 열거형과 속성을 가지고 특정 기능을 수행하는 `메서드`를 열거형 안에 정의해둘 수도 있다.

```java
public enum Type {
    NORTH("북쪽"),
    EAST("동쪽"),
    SOUTH("남쪽"),
    WEST("쪽");

    private final String korean;

    Type(String korean) {
        this.korean = korean;
    }
    
    public Type getType(String korean) {
        return valueOf(korean);
    }
}
```

### 열거형의 생성자

이 때, 생성자의 접근 제어자는 `private`으로 다른 제어자로 변경할 수 없다.

<img width="489" alt="열거형 생성자 public 안됨" src="https://user-images.githubusercontent.com/47437757/179400006-d8ada0c8-c66d-4d61-bc5a-b489015d89d3.png">

<img width="211" alt="열거형 생성자 private" src="https://user-images.githubusercontent.com/47437757/179400004-9643af37-8319-4d59-aca5-424c65263cd8.png">

<aside>
💡 Enum은 클래스와 동급이지만, 인스턴스로 만들어 쓸 수 없다. 다른 용도로 사용하는 것을 금지하고 있다고 볼 수 있다.

</aside>

## Enum이 제공하는 메서드

- values()
    - 열거형의 모든 상수를 배열에 담아 반환한다.
- valueOf()
    - 지정된 열거형에서 name과 일치하는 열거형 상수를 반환해서, 해당 상수에 대한 참조를 얻을 수 있게 해준다.
- ordinal()
    - 열거형 상수가 정의된 순서를 반환한다.
- name()
    - 열거형 상수의 이름을 문자열로 반환한다.
- getDeclaringClass()
    - 열거형의 Class객체를 반환한다.

## java.lang.Enum

모든 열거형의 조상이다.

Enum 클래스는 `추상 클래스`로 Enum 클래스의 인스턴스를 생성할 수 없다.

Enum이 기본적으로 제공하는 메서드들은 

모두 이 java.lang.Enum 클래스에 정의되어 있는 것들이며, final로 제공되어 수정할 수 없다.

```java
public abstract class Enum<E extends Enum<E>>
        implements Constable, Comparable<E>, Serializable {
    private final String name;
		public final String name() {
        return name;
    }

		private final int ordinal;
    public final int ordinal() {
        return ordinal;
    }

	...
}
```

## EnumSet

Enum 클래스와 함께 사용하기 위해 만들어진 Set 컬렉션이다.

AbstractSet을 상속함으로써 Set 인터페이스를 구현하고 있다.

EnumSet의 내부는 비트 벡터로 구현되어 있다.

<img width="595" alt="EnumSet 구조" src="https://user-images.githubusercontent.com/47437757/179400009-57403d1a-9d59-4a3d-8a75-6e9639032116.png">

EnumSet은 인스턴스를 생성할 수 있는 몇가지 정적 팩토리 메서드를 제공하는데

그를 사용해서 필요한 열거형을 중복을 허용하지 않으며, 순서가 없는 Set 컬렉션으로 다룰 수 있다.

### 속도가 빠르고 메모리를 덜 사용한다.

EnumSet의 모든 메서드는 산술 비트 연산을 사용해서 계산이 매우 빠르다.

HashSet과 같은 다른 Set 구현과 비교하면 값이 예측 가능한 순서로 저장되고 

각 계산에 대해 하나의 비트만 검사하며 되기 때문에 일반적으로 더 빠르다.

또한 HashSet과 달리 올바른 버킷을 찾기 위해 해시코드를 계산할 필요가 없다.

EnumSet은 비트 벡터의 특성으로 인해 메모리를 덜 사용한다.

### 메서드

- allOf
    - 해당 열거형의 모든 요소를 갖는 EnumSet 생성
- noneOf
    - 해당 열거형의 빈 컬렉션을 갖는 EnumSet 생성
- complementOf
    - 원하는 요소를 뺴고 해당 열거형의 나머지 요소를 갖는 EnumSet 생성
- copyOf
    - 다른 EnumSet의 모든 요소를 복사해서 EnumSet 생성
- contains
    - 특정 요소가 EnumSet에 포함되어 있는지 확인
- add
    - EnumSet에 요소 추가
- remove
    - EnumSet에서 특정 요소 제거

# Annotation

자바에선 어노테이션을 사용해서 소스 코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킬 수 있다.

어노테이션엔 기본적으로 제공되는 것들과 그 외 메타 어노테이션들이 있다.

메타 어노테이션들로 커스텀 어노테이션을 정의할 수 있다.

## 정의하기

주로 java.lang.annotation 패키지에 있는 4가지 어노테이션을 이용하여 작성한다.

이를 통해 어노테이션의 적용대상이나 유지기간 등을 지정할 수 있다.

- @Retention
    - 어노테이션의 유지 기간을 지정한다.
    - 유지 정책은 `RententionPolicy`에 정의되어 있으며 종류는 `SOURCE`, `CLASS`, `RUNTIME`이 있다.
        - SOURCE : 소스 파일에만 존재. 클래스 파일에는 존재하지 않음
        - CLASS : 클래스 파일에 존재. 실행시에 사용불가. 기본값
        - RUNTIME : 클래스 파일에 존재. 실행시에 사용가능
- @Target
    - 어노테이션이 적용 가능한 대상을 지정
    
    ```java
    @Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE, MODULE})
    @Retention(RetentionPolicy.SOURCE)
    public @interface SuppressWarnings {
    	...
    }
    ```
    
- @Documented
    - 어노테이션에 대한 정보가 javadoc로 작성한 문서에 포함되도록 한다.
- @Inherited
    - 어노테이션이 해당 어노테이션을 쓴 부모의 자손 클래스에 상속되도록 한다.

### 커스텀 어노테이션

커스텀 어노테이션을 만들기 위해선 지켜야 할 규칙이 몇가지 있다.

- 어노테이션의 타입은 @interface이다.
- 

## 어노테이션 프로세서

참고

[1] [https://www.baeldung.com/java-enumset](https://www.baeldung.com/java-enumset)  

[2] [https://www.geeksforgeeks.org/java-lang-enum-class-java/](https://www.geeksforgeeks.org/java-lang-enum-class-java/)  

[3] [https://scshim.tistory.com/253](https://scshim.tistory.com/253)  

[4] [https://donghyeon.dev/spring/2020/08/18/Spring-Annotation의-원리와-Custom-Annotation-만들어보기/](https://donghyeon.dev/spring/2020/08/18/Spring-Annotation%EC%9D%98-%EC%9B%90%EB%A6%AC%EC%99%80-Custom-Annotation-%EB%A7%8C%EB%93%A4%EC%96%B4%EB%B3%B4%EA%B8%B0/)
