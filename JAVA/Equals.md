# equals()
Object 클래스의 객체의 주소 비교 메서드
내부적으로 참조값을 비교한다.
일반적으로 문자열 비교를 위해서 사용하는 equals()는 String 클래스에서 오버라이딩한 메서드로 값의 비교를 수행한다.

# == 연산자
객체의 주소값을 비교
비교하는 객체가 동일한 객체인지 판별한다.
기본형 객체에 대해서는 값 비교, 참조형 객체에 대해서는 메모리 주소 비교를 수행한다.

```java
Integer a = 100;
Integer b = 100;

System.out.println(a == b); // true
```
위 코드와 같이 참조형임에도 == 연산자로 true가 반환되는데 이는 JVM이 자주 사용되는 범위의 Integer등 참조형 객체를 캐싱한다.
따라서 캐싱된 객체이기 때문에 메모리 주소값이 같아 true가 반환된다.

## 문자열에서의 equal과 == 연산자
```java
String str1 = "String";
String str2 = "String";
String str3 = new String("String");
String str4 = new String("String");
```

str1과 str2는 String Constant Pool에 등록된 `String` 문자열을 참조하기 때문에 == 비교에서 true를 반환한다.
str3과 str4는 힙 영역에 문자열 객체를 각각 새로 생성하기 때문에 == 비교에서 false를 반환하기 때문에
값 자체를 비교하기 위해서 equals() 메서드를 사용해야한다.
