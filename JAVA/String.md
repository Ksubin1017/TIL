# String
문자열이라고 불리는 클래스
int, long 등 기본형 타입과 달리 참조형으로 분류되며 객체와 같이 힙에 문자열 데이터가 생성된다.

## 불변(Immutable)
자바는 기본적으로 String 객체의 값을 변경할 수 없다.

```java
String str = "Hello ";
str += "World!";

System.out,println(str); // Hello World!
```

위 예시 코드를 보면, 힙 영역에 생성된 `Hello `의 값을 `Hello World!`로 변경하는 것처럼 보인다.
실제로는 힙 영역에 `Hello World!`를 새로 생성하고 변수 a는 이를 참조한다.

### 불변의 이유
JVM은 String Constant Pool이라는 여영역을 따로 만들고 생성되는 문자열들을 관리한다.
String Constant Pool에서 관리되는 문자열들은 다른 변수 및 객체들과 공유하게 되고 데이터 캐싱을 통한 성능적 이득을 취할 수 있다.

데이터가 불변이면 멀티 스레드 환경에서 동기화 문제가 발생하지 않기 때문에 스레드 safe 결과를 낼 수 있다.
또한 데이터베이스의 사용자 이름, 암호 등은 문자열로 전달되는데 이 값을 변경이 가능하다면 참조 값을 변경해 애플리케이션에 문제를 야기시킬 수 있게된다.

## 주소할당과 String Constant Pool
```java
// 문자열 리터럴
String str1 = "Hello";
String str2 = "Hello";

// new 연산자
String str3 = new String("Hello"); 
String str4 = new String("Hello");
```
str1과 str2는 String Constant Pool에 저장되어 관리되지만 new를 통해 생성한 str3, str4는 힙 영역에 String 객체를 새로 생성한다.
따라서 str1과 str2는 같은 메모리 주소를 가리키고, str3와 str3의 메모리 주소는 다르다.

일반적으로 new를 사용하지않고 문자열 리터럴을 통한 개발 방식을 사용하는데, 문자열의 경우 재사용성이 높기 때문에 String Constant Pool에서 관리하는 객체를
공유하면 메모리를 절약할 수 있다.

## 문자열의 연산
### `+` 연산
```java
String str = "Hello ";
str = new StringBuilder(str)
        .append("World!")
        .toString();
```
`+`를 통한 연산을 사용하게 되면 내부적으로 위 코드와 같이 StringBuilder를 생성하고 새 String 객체를 생성하게 되기에 성능이 저하된다.
따라서 문자열 변경이 잦다면 지양해야하는 방식이다.

```java
String s = "Hello " + "World";

String a = "Hello ";
String s = a + "World";  
```
다만, 컴파일 타임에 연산을 미리 지정하면 컴파일러에 의해 연산 결과가 바로 저장되지만 변수를 사용하게 된다면 런타임에 StringBuilder를 사용한다.

### StringBuilder
가변 문자열 객체로 문자열을 직접 변경
```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < n; i++) {
    sb.append(i);
}
String s = sb.toString();  
```

`+` 연산 시 StringBuilder를 사용한다면 `+`와 StringBuilder는 성능이 같다고 생각할 수도 있다.
핵심은 StringBuilder를 몇 번 생성하느냐이다.
`+`의 경우 연산마다 StringBuilder를 생성하여 문자열을 연산하기 때문에 메모리가 낭비되는 등 성능이 저하된다.

반면 StringBuilder를 통해 연산을 수행할 경우 StringBuilder를 재사용하기 때문에 메모리를 절약할 수 있다.
따라서 문자열 변경이 자주 일어난다면 StringBuilder를 사용하는 것이 좋은 선택이다.

### StringBuffer
가변 문자열 객체로 문자열을 직접 변경
멀티스레드 환경에서 여러 스레드가 문자열을 수정할 경우에 대비해 만들어졌다.
StringBuilder와 문자열을 다루는 API가 거의 동일하다. 
```java
StringBuffer sb = new StringBuffer();
for (int i = 0; i < n; i++) {
    sb.append(i);
}
String s = sb.toString();  
```

## StringBuilder vs StringBuffer
두 객체의 차이점은 동기화에 있다.
StringBuffer의 경우 제공하는 메서드에 synchronized 키워드를 사용하여 동기화에 이점이 있고 멀티스레드 환경에서 안정적이다.

하지만 동기화 오버헤드(락 획득, 해제 등)으로 인해 StringBuilder보다는 성능이 떨어진다.
