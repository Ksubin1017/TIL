# 제네릭
결정되지 않은 타입을 파라미터로 처리하고 실제 사용할 때 파라미터를 구체적인 타입으로 대체 시키는 기능

```java
public class Box<T> {
    public T content;
}

Box<String> box = new Box<String>();
```
`<T>`는 T가 파라미터임을 뜻하는 기호로 타입이 필요한 자리에 T를 사용할 수 있음을 알려주는 역할을 한다.
Box 클래스는 T가 무엇인지 모르지만 Box 객체가 생성될 시점에 다른 타입으로 대체된다는 것은 알고 있다.

## 이점
제네릭을 사용하면 컴파일 시 강한 타입 체크가 가능하다. 런타임 시의 타입 에러보다 컴파일 시에 미리 타입을 체크하여 코드 상 문제점을 방지할 수 있다.

## 제네릭 타입
결정되지 않은 타입을 파라미터로 가지는 클래스와 인터페이스

타입 파라미터는 변수명과 동일한 규칙에 따라 작성할 수 있지만 일반적으로 대문자 알파벳 한 글자로 표현한다.
외부에서 제네릭 타입을 사용하려면 타입 파라미터에 구체적인 타입을 지정해야하는데, 지정하지 않는다면 Object 타입이 암묵적으로 사용된다.

## 제네릭 메서드
타입 파라미터를 가지고 있는 메서드
타입 파라미터가 메서드 선언부에 정의된다는 점에서 제네릭 타입과는 차이가 있다.

```java
public class Box {
    public static <T> T pick(T value) {
        return value;
    }
}

// 사용
String s = Util.<String>pick("test");
Integer i = Util.pick(123);
```

제네릭 메서드는 메서드를 호출할 때마다 타입을 다르게 쓸 수 있다.
위 코드 예시처럼 하나의 타입만을 리턴하는 것이 아닌 메서드에서 독립적으로 타입을 제어할 수 있다.
따라서 여러 타입을 입력받는 유틸리티 메서드를 만들 때 유용하다.

```java
public static <T extends Comparable<? super T>> void sort(List<T> list)
```
Collections.sort()처럼 어떤 타입의 리스트든 정렬이 가능하게끔 메서드를 구현할 수 있다.

## 주의점
```java
T t = new T();
```
제네릭 타입 자체로 타입을 지정하여 객체를 생성하는 것은 불가능 하다.

```java
class Box<T> {
    private int height;
    private int weight;

    public static T setHeight(int n) {
    }
}
```
static은 클래스 로딩 시점에 메모리에 올라가며 타입이 정해지기 때문에 클래스 로딩이 되는 순간 setHeight()는 완성된 형태여야한다.
하지만 제네릭 타입은 객체 생성 시점에 결정되기 때문에 에러가 발생하게 된다.
