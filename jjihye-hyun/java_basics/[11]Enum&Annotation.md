# Enum(열거형)
enum은 서로 관련된 상수를 편리하게 선언하기 위한 것으로 여러 상수를 정의할 때 유용하다. 값과 타입을 체크하기 때문에 타입에 안전하다는 특징이 있고, 상수의 값이 바뀌어도 기존 소스를 다시 컴파일 하지 않아도 된다. 
## Enum 정의하는 방법
```java
enum 열겨형이름 { 상수명1, 상수명2 ... }
```
```java
enum Direction { EAST, SOUTH, WEST, NORTH }
```
### 열겨형에 정의된 상수 사용하는 방법
```java
// 열거형이름.상수명
Direction dir = Direction.NORTH;
```
- 비교연산자 '==' 사용 가능, '<' '>' 사용할 수 없음
- compareTo()사용가능 (같으면 0, 왼쪽이 크면 양수, 오른쪽이 크면 음수)
```java
if(dir==Direction.NORTH){
    x++;
} else if(dir > Direction.SOUTH){
    // 에러, 열거형 상수에 비교연산자 사용불가
} else if(dir.compareTo(Direction.SOUTH) > 0){
    // 사용 가능
}
```
- switch문 조건식에 사용가능. 열거형 이름을 적지 않고 상수 이름만 적어야 한다.
```java
switch(dir){
    case EAST: x++;
        break;
    case WEST: x--;
        break;
}
```

## java.lang.Enum
- 모든 열거형의 조상
### Enum이 제공하는 메소드
| 메서드 | 설명 |
| ---- | ---- |
| Class<E> getDeclaringClass() | 열거형의 Class객체를 반환한다. |
| String name() | 열거형 상수의 이름을 문자열로 반환한다. |
| int ordinal() | 열거형 상수가 정의된 순서를 반환한다.(0부터 시작) |
| T valueOf(Class<T> enumType, String name) | 지정된 열거형에서 name과 일치하는 열거형 상수를 반환한다. |
| T[] values() | 열거형의 모든 상수를 배열에 담아 반환한다. |


## EnumSet
enum 형으로 사용하기 위한 특수한 Set이다.
### 특징 
-  java.util 패키지에 정의되어 있으며, Set 자료구조의 특징을 따른다.
```java
import java.util.EnumSet; 

public class CarClass {   
     public static void main(String[] args) {        
        EnumSet<CarBrand> carBrands = EnumSet.allOf(CarBrand.class);        // 모든 요소를 포함한 EnumSet 반환         
        EnumSet<CarBrand> koreaBrand = EnumSet.of(CarBrand.HYUNDAI, CarBrand.KIA, CarBrand.SSANGYONG);        // 특정 상수만 포함한 EnumSet 반환         
        EnumSet<CarBrand> germanyBrand = EnumSet.complementOf(koreaBrand);        // 특정 상수를 제외한 EnumSet 반환         
        EnumSet<CarBrand> kia_Audi = EnumSet.range(CarBrand.KIA, CarBrand.AUDI);        // 특정 범위의 EnumSet 반환 ( Kia ~ Audi )         
        System.out.println(carBrands);        
        System.out.println(koreaBrand);        
        System.out.println(germanyBrand);        
        System.out.println(kia_Audi);    
    }
}
enum CarBrand {    HYUNDAI, KIA, SSANGYONG, BENZ, AUDI, BMW}

/*
[HYUNDAI, KIA, SSANGYONG, BENZ, AUDI, BMW]
[HYUNDAI, KIA, SSANGYONG]
[BENZ, AUDI, BMW]
[KIA, SSANGYONG, BENZ, AUDI] 
*/
```

# Annotation
- 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것
- 컴파일러에게 유용한 정보 제공함(<code>@Overrride</code>)

## 애노테이션 정의하는 방법
```java
@interface 애너테이션이름{
    타입 요소이름(); //애너테이션의 요소를 선언한다.
}
```
```java
public @interface MyAnnotation { }
```
사용
```java
@MyAnnotation
```
어노테이션은 클래스의 필드처럼 엘리먼트를 멤버로 가질 수 있다. 
각 엘리먼트는 타입과 이름으로 구성되며,디폴트 값을 가질 수 있다. 디폴트 값이 있으면 사용시에 생략가능하다. 엘리먼트 타입으로는 int나 double과 같은 원시 타입이나 String, Class 타입, 그리고 이들의 배열 타입을 사용할 수 있다.
```java
public @interface MyAnnotation {    
    String value();    
    int number() default 10;}
```
사용
```java
@MyAnnotation(value = "coco")
public class AnnotationTest { }
```
```java
@MyAnnotation(value = "coco", number = 1)
public class AnnotationTest { }
```


## @retention
메타 애너테이션은 에너테이션을 위한 에너테이션, 즉, 애너테이션에 붙이는 애너테이션으로 애너테이션을 정의할 때 사용한다. @retention, @target, @documented 이 포함된다.

@retiention은 애너테이션이 유지되는 기간을 지정하는데 사용된다.
### 유지 정책 종류
| 유지정책 | 의미 |
| ----- | ---- |
| SOURCE | 소스파일에만 존재, 클래스파일에는 존재하지 않음 |
| CLASS | 클래스 파일에 존재, 실행시에 사용불가. 기본값 |
| RUNTIME | 클래스 파일에 존재, 실행시에 사용가능 |

## @target
애너테이션이 적용가능한 대상을 지정하는데 사용된다. 
```java
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
```
### 적용대상 종류
| 대상타입 | 의미 |
| ----- | ---- |
| ANNOTATION_TYPE | 애너테이션 |
| CONSTRUCTOR | 생성자 |
| FIELD | 핃드(멤버변수, enum 상수) |
| LOCAL_VARIABLE | 지역변수 |
| PACKAGE | 패키지 |
| PARAMETER | 매개변수 |
| TYPE | 타입(클래스, 인터페이스, enum) |
| TYPE_PARAMETER | 타입 매개변수 |
| TYPE_USE | 타입이 사용되는 모든 곳 |

## @documented
애너테이션에 대한 정보가 javadoc으로 작성한 문서에 포함되도록한다. 자바에서 제공하는 기본 애너테이션 중에 @Override, @SuppressWarning을 제외하고는 모두 붙어있다.

## 애노테이션 프로세서
annotation processor는 자바 컴파일러 플러그인의 일종으로, 어노테이션에 대한 코드베이스를 검사, 수정, 생성하는 역할이다.
어노테이션을 사용하기 위해서는 어노테이션 프로세서가 필요하다.
 
### 동작 구조
1. 어노테이션 프로세서를 사용한다는 것을 자바 컴파일러가 알고 있는 상태에서 컴파일을 수행
2. 어노테이션 프로세서들이 각자의 역할에 맞게 구현되어 있는 상태에서 실행되지 않은 어노테이션 프로세서를 실행
3. 어노테이션 프로세서 내부에서 어노테이션에 대한 처리
4. 자바 컴파일러가 모든 어노테이션 프로세서가 실행 되었는지 검사하고, 모든 어노테이션 프로세서가 실행되지 않았다면 반복


---
### 참고
- 자바의 정석
- https://scshim.tistory.com/253
- https://dev-coco.tistory.com/24