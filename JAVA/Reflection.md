# 리플렉션
메타 정보를 프로그램에서 읽고 수정하는 행위

자바는 클래스와 인터페이스의 메타 정보를 Class 객체로 관리한다.
메타 정보란 패키지 정보, 타입 정보, 멤버(생성자, 필드, 메서드) 정보 등을 의미한다.

힙 영역에 로드된 Class 타입의 객체를 통해 접근 제어자와 관계없이 원하는 클래스 정보에 접근 및 조작할 수 있도록 API를 지원한다.

스프링같은 프레임워크가 객체를 자동 생성할 때 스프링은 개발자가 코드를 작성하는 시점에 어떤 클래스가 있는지 알 수 없다.
따라서 클래스 스캔, 생성자 호출 등의 작업을 리플렉션으로 동적으로 처리한다.

어노테이션을 기반으로 기능을 생성할 때, Jackson 혹은 Gson등 객체 변환 라이브러리가 Json 필드 이름과 자바 필드 이름을 런타임에 매핑할 때
리플렉션으로 동작한다.

프로그램에서 Class 객체를 얻으려면 아래 3가지 방법을 사용한다.
```java
1. Class clazz = 클래스명.class;
2. Class clazz = Class.forName("패키지...클라스이름");
3. Class clazz = 객체참조변소.getClass();
```
1, 2번은 클래소르부터, 3번은 객체로부터 Class 객체를 얻는 방법이다.

### 장점
- 구체적인 클래스를 알지 못해도 동적으로 클래스를 생성해 의존 관계를 맺을 수 있다.
- 접근 제한과 관계없이 테스트가 가능하다.

### 단점
- 캡슐화가 저해될 우려가 있다.
- 리플렉션을 통한 접근이 대부분 느려 성능이 저하될 수 있다.
- 런타인 단계에서 에러가 발생하면서 디버깅이 어려워진다.
  
## 패키지와 타입 정보 얻기
Pakage getPackeage()  패키지 정보 읽기
String getSimpleName() 패키지를 제외한 타입 이름
String getName() 패키지를 포함한 전체 타입 이름

## 멤버 정보 얻기
Constructor[] getDeclaredConstructors() 생성자 정보 읽기
Field[] getDeclaredFields() 필드 정보 읽기
Method[] getDeclaredMethods() 메서드 정보 읽기

각각 생성자 배열, 필드 배열, 메서드 배열을 리턴한다. 
Constructor, Field, Method 클래스는 모드 java.lang.reflect 패키지에 있으며 각각 생성자, 필드, 메서드에 대한 선언부 정보를 제공한다.

## 리소스 경로 얻기
URL getResource(String name) 리소스 파일의 URL 리턴
InputStream getResourceAsStream(String name) 리소스 파일의 InputStream 리턴
