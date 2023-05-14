# 컬렉션 API 개선

## 컬렉션 팩토리(자바 9)
작고 변경되지 않는 데이터인 경우 사용

### 1. 리스트 팩토리
<code>List.of</code>: 바꿀 수 없는 List 만드는 팩토리 메서드

- 요소 추가, 삭제 X
- 요소 값 변경 X
- null 요소 허용 하지 않음

```java
List list = List.of("a", "b", "c");
//list.add("d");   // java.lang.UnsupportedOperationException
//list.set(0, "d");  // java.lang.UnsupportedOperationException
System.out.println(list);  //[a, b, c]
```
[VS Arrays.asList](https://jaehoney.tistory.com/144)
```java
List<String> friends = Arrays.asList("a", "b", "c");
//friends.add("d");    // java.lang.UnsupportedOperationException
friends.set(0, "d");   // 값 변경 가능     
System.out.println(friends);  // [d, b, c]
```

### 2. 집합 팩토리
<code>Set.of</code>: 바꿀 수 없는(불변객체) 집합 만드는 팩토리 메서드

- 집합은 고유한 요소만 포함함. 중복 원소 없음

```java
//java.lang.IllegalArgumentException: duplicate element: c
//Set<String> friends = Set.of("a", "b", "c", 'c");   

Set<String> friends = Set.of("a", "b", "c");  
friends.add("d");  //java.lang.UnsupportedOperationException
System.out.println(friends);
```

### 3. 맵 팩토리
<code>Map.of</code>: 바꿀 수 없는 맵 초기화 팩토리 메서드

1. 10개 이하의 키-값 쌍을 가진 맵을 만들 때
Map.of 팩토리 메서드에 키, 값 번갈아 입력
```java
Map<String, Integer> ageOfFriends = Map.of("a", 20, "b",20, "c", 21);
System.out.println(ageOfFriends);  //{a=20, b=20, c=21}
```

2. 10개 이상인 경우
Map.ofEntries 팩토리 메서드 사용하는 것이 유리   
Map.enrty<K,V> 객체를 인수로 받음.
```java
Map<String, Integer> ageOfFriends = Map.ofEntries(
                Map.entry("a", 20),
                Map.entry("b",20),
                Map.entry("c", 21));
System.out.println(ageOfFriends);  //{a=20, b=20, c=21}
```
## 리스트와 집합처리
자바8에서 List, Set 인터페이스 메서드에 다음과 같은 메서드를 추가했다. 이 메서드들은 호출한 컬렉션 자체를 바꾼다.
- removeIf: Predicate를 만족하는 요소 제거한다. List, Set에서 사용 가능
- replaceAll: UnaryOperator 함수(입력받은 파라미터 타입과 리턴 받는 타입이 동일한 Functional Interface)를 이용해 요소 바꿈. List에서 사용 가능
- sort: 리스트 정렬. List에서 사용 가능

### 1. removeIf 메서드
removeIf 메서드는 삭제할 요소를 가리키는 프리디케이트를 인수로 받는다.
```java
List<String> friends = new ArrayList<>();
friends.add("a");
friends.add("b");
friends.add("c");

friends.removeIf(friend -> friend.equals("a"));
        
System.out.println(friends);  //[b, c]
```
코드복잡, 오류 발생 가능성 존재.
```java
for (String friend: friends){
    if(friend.equals("a")){
        friends.remove(friend); //java.util.ConcurrentModificationException 발생!
    }
}
```
내부적을 for-each는 Interator 객체를 사용한다.
- Iterator 객체. next(), hasNext()를 이용하여 질의
- Collection 객체 자체 remove()를 호출해서 요소 삭제
반복자 상태와 컬렉션 상태가 서로 동기화하지 않아서 오류 발생 
```java
for (Iterator<String> iterator = friends.iterator(); iterator.hasNext();) {
    String friend = iterator.next();
    if(friend.equals("a")){
        friends.remove(friend);  //java.util.ConcurrentModificationException 발생!
    }
}
```
```java
for (Iterator<String> iterator = friends.iterator(); iterator.hasNext();) {
    String friend = iterator.next();
    if(friend.equals("a")){
        iterator.remove();  //iterator 객체를 삭제하도록 명시
    }
}
System.out.println(friends);  //[b, c]
```

### 2. replaceAll 메서드
replaceAll 메서드는 리스트의 각 요소를 새로운 요소로 바꿀 수 있다.   

- 스트림 API를 이용한 경우
기존 컬렉션 자체를 바꾸는 것이 아니라 새 문자열 컬렉션을 만듬.
```java
friends.stream().map(friend -> Character.toUpperCase(friend.charAt(0)))
                .collect(Collectors.toList())
                .forEach(System.out::println); // A,B,C

System.out.println(friends); //[a,b,c]
```
- ListIterator 객체 이용
코드 복잡. 컬렉션 객체와 Iterator 객체 혼용하면서 반봅과 컬렉션 변경 동시에 이루어짐
```java
for(ListIterator<String>  iterator = friends.listIterator(); iterator.hasNext();){
    String friend = iterator.next();
    iterator.set(String.valueOf(Character.toUpperCase(friend.charAt(0))));
}
System.out.println(friends); //[A,B,C]
```
```java
friends.replaceAll(friend -> String.valueOf(Character.toUpperCase(friend.charAt(0))));
System.out.println(friends); //[A,B,C]
```

## 맵 처리
자바 8에서 Map인터페이스에 디폴트 메서드 추가됨.

### 1. forEach 메서드
맵에서 키와 값을 반복적으로 확인 하는 작업이 필요할 때

- Map.Entry 반복자 이용
```java
Map<String, Integer> ageOfFriends = Map.of("a", 20, "b", 20, "c", 21);

for(Map.Entry<String, Integer> entry : ageOfFriends.entrySet()){
    String friend = entry.getKey();
    Integer age = entry.getValue();
    System.out.println(friend + " is " + age + "years old");
}
/*
a is 20years old
b is 20years old
c is 21years old
*/
```
- forEach 메서드 이용
```java
ageOfFriends.forEach((friend, age) -> System.out.println(friend + " is " + age + "years old"));
/*
a is 20years old
b is 20years old
c is 21years old
*/
```
자바 8에서부터 Map 인터페이스는 BiConsumer(키,값)를 인수로 받는 forEach 메서드 지원
```java
default void forEach(BiConsumer<? super K, ? super V> action) {
    Objects.requireNonNull(action);
    for (Map.Entry<K, V> entry : entrySet()) {
        K k;
        V v;
        try {
            k = entry.getKey();
            v = entry.getValue();
        } catch (IllegalStateException ise) {
            // this usually means the entry is no longer in the map.
            throw new ConcurrentModificationException(ise);
        }
        action.accept(k, v);
    }
}
```

### 2. 정렬 메서드
맵의 항목을 값 또는 키를 기준으로 정렬 할 때
- Entry.comparingByValue
- Entry.comparingByKey
```java
ageOfFriends.entrySet()
.stream()
.sorted(Map.Entry.comparingByKey())  //알파벳 순으로
.forEachOrdered(System.out::println);
/*
a=20
b=20
c=21
*/
```

### 3. getOrDefault 메서드
요청한 키가 맵에 존재하지 않을 때 null이 반환되어 NullPointerException 발생함.   
이를 반지하기 위채 요청한 키가 맵에 존재 하지 않을 때, 기본값으로 반환하도록 하는 메서드.   
첫번째 인수: 키, 두번째 인수: 기본값
```java
System.out.println(ageOfFriends.getOrDefault("d", 0)); //0
```
키가 존재 하더라고요 값이 null인 경우, getOrDefault도 null를 반환할 수 있음.

### 4. 계산 패턴
맵에 키가 존재하는지 여부에 따라 어떤 동작을 실행하고 결과를 저장해야할 때
- computeIfAbsent: 제공된 키에 값이 없으면, 키를 이용해서 새 값을 계산하고 맵에 추가
- computeIfPresent: 제공된 키가 존재하면, 새 값을 계산하고 맵에 추가
- comput: 제공된 키로 새 값을 계산하고 맵에 저장
``` java
Map<Integer, Integer> map = new HashMap<>();
map.put(1,2);
map.put(2,4);

// key 3 이 없으므로 연산 후 추가
map.computeIfAbsent(3, key-> key*2);
System.out.println(map);  //{1=2, 2=4, 3=6}
// key 3 존재 하므로 연산 하지 않음
map.computeIfAbsent(3, key-> key*2);
System.out.println(map);  //{1=2, 2=4, 3=6}

// key 4 가 없으므로 값 추가 안함
map.computeIfPresent(4, (key,value) -> key*2);
System.out.println(map);  //{1=2, 2=4, 3=6}
// key 3이 존재하므로 새 값 추
map.computeIfPresent(3, (key,value) -> key*3);
System.out.println(map);  //{1=2, 2=4, 3=9}

// key 3 으로 연산
map.compute(3, (key,value) -> key*4);
System.out.println(map);  //{1=2, 2=4, 3=12}
```
Map<k, List<V>> 같은 경우 요소 추가 하려고 할때, 초기화 여부 확인 할때 유용
```java
Map<String, List<String>> map2 = new HashMap<>();
// key a 가 없으므로 new ArrayList<>() 반환
map2.computeIfAbsent("a", name -> new ArrayList<>()).add("Rachel"); //{a=[Rachel]}
```

### 5. 삭제 패턴
제공된 키에 해당하는 맵 항복 제거할 때   
java8에서는 키가 특정한 값과 연관되었을 때만 항목을 제거하는 오버로드 버전 메서드를 제공한다.
```java
// map.remove(key, value)
map.remove(3, 12);
```
### 6. 교체 패턴
맵 항목을 바꿀 때
- replaceAll: BiFunction을 적용한 결과로 각 항목의 값을 교체한다.
- Replace: 키가 존재하면 맵의 값을 바꾼다. 키가 특정 값으로 매핑 되었을 때만 값을 교체하는 오버로드 버전도 제공
```java
Map<String, String> favouriteMovies = new HashMap<>();
favouriteMovies.put("Raphael", "Star Wars");
favouriteMovies.put("Olivia", "james bond");
favouriteMovies.replaceAll((friend, movie) -> movie.toUpperCase()); // {Olivia=JAMES BOND, Raphael=STAR WARS}

favouriteMovies.replace("Olivia", "inception"); //{Olivia=inception, Raphael=STAR WARS}
// replace(key, oldvalue, newvalue)
favouriteMovies.replace("Olivia", "inception", "INCEPTION"); //{Olivia=INCEPTION, Raphael=STAR WARS}
```

### 7. 합침
두 개의 맵을 합치거나 바꿀 때 forEach와 merge 사용
```java
Map<String, String> family = Map.ofEntries(
    Map.entry("Raphael","Star Wars"),
    Map.entry("Olivia", "james bond")
);

Map<String, String> friends = Map.ofEntries(
    Map.entry("Olivia","inception"),
    Map.entry("Jasmin", "The Avengers")
);

Map<String, String> everyOne = new HashMap<>(family);
// 중복 키 있을 때 어떻게 합칠 지 BiFunction을 인수로 받은
// merge(key, value, remappingFunction(recompute value))
friends.forEach((k, v) -> everyOne.merge(k,v,(movie1, movie2) -> movie1 + " & " + movie2));
// {Olivia=james bond & inception, Jasmin=The Avengers, Raphael=Star Wars}
```

## 개선된 ConcurrentHashMap
ConcurrentHashMap는 동시성 친화적(multi thread)이며 최신 기술을 반영한 HashMap 버전이다. 
ConcurrentHashMap는 내부 자료구소의 특정 부분만 잠궈 동시 추가, 갱신 작업을 허용한다.

### 1. 리듀스와 검색
- forEach: 각 키,값 쌍에 주어진 액션 실행
- reduce: 모든 키, 값 쌍을 제공된 리듀스 함수를 이용해 결과로 합침
- search: 널이 아닌 값을 반환할 때까지 각 키,값 쌍에 함수 적용
다음와 같이 4가지 연산 형태 제공
- 키,값으로 연산(forEach, reduce, search)
- 키로 연산(forEachKey, reduceKey, searchKey)
- 값으로 연산(forEachValue, reduceValue, searchValue)
- Map.Entry객체로 연산(forEachEntry, reduceEntry, searchEntry)

연산은 ConcurrentHashMap의 상태를 잠그지 않고 연산 수행. synchronized 키워드가 선언되어 있진 않다.따라서 이들 연산에 제공한 함수는 계산이 진행되는 동안 바뀔 수 있는 객체, 값, 순서 등에 의존하지 않아야 함.   
또한 이들 연산에 병렬성 기준값을 지정해야 한다. 맵의 크기가 주어진 기준값보다 작으면 순차적으로 연산을 실행한다.
기준값을 1로 지정하며 공통 스레드 풀을 이용해 병렬성을 극대화한다.   
Long.MAX_VALUE를 기준값으로 설정하면 한 개의 스레드로 연산을 실행한다.   
소프트웨어 아키텍처가 고급 수준의 자원 활용 최적화를 사용하고 있지 않다면 기준값 규칙을 따르는 것이 좋다.   
### 2. 계수
ConcurrentHashMap 클래스는 맵의 매핑 개수를 반환하는 mappingCount 메서드를 제공한다.   
기존의 size 메서드 대신 새 코드에서는 int를 반환하는 mappingCount 메서드를 사용하는 것이 좋다. 그래야 매핑의 개수가 int의 범위를 넘어서는 이후의 상황을 대처할 수 있기 때문이다.
```java
ConcurrentHashMap<String, String> familyMap = new ConcurrentHashMap<>();
familyMap.put("Raphael","Star Wars");
familyMap.put("Olivia", "james bond");
        
System.out.println(familyMap.mappingCount()); //2
```
### 3. 집합뷰
- KeySet: ConcurrentHashMap을 집합 뷰로 반환하는 메서드. 
- newKeySet: ConcurrentHashMap을 유지하고 새로운 집합 생성하는 메서드
```java
Set familySet = familyMap.keySet(); //[Olivia, Raphael]
Set newfamilySet = familyMap.newKeySet(); //[]
```