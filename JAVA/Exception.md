# 예외
잘못된 사용 또는 코딩으로 인한 오류

일반 예외(Exception): 컴파일러가 예외 처리 코드 여부를 검사하는 예외
실행 예외(Runtime Exception): 컴파일러가 예외 처리 코드 여부를 검사하지 않는 예외

자바는 예외가 발생하면 예외 클래스로부터 객체를 생성하고 이 객체는 예외  처리 시 사용된다.
자바의 모든 에러와 예외 클래스는 Throwable을 상속받아 만들어지고 예외 클래스는 java.lang.Exception 클래스를 상속받는다.

## Checked Exception
반드시 처리해야하는 예외로 컴파일러가 강제하는 예외
try-catch 또는 throws로 예외를 던져야 컴파일이 가능하다.
IOException, SQLException, ClassNotFountException 등이 있다.

## Unchecked Exception
처리하지 않아도 되는 예외로 컴파일러가 강제하지 않고 런타임에 터지는 예외
대부분 RuntimeException을 상송한다.
NullPointerException, IllegalArgumentException,IndexOutOfBoundsException 등이 있다.

## 예외 처리 코드
예외가 발생했을 때 프로그램의 갑작스러운 종료를 막고 정상 실행을 유지할 수 있도록 하는 코드
try-catch-finally 블록으로 구성되며 생성자 내부와 메서드 내부에 작성된다.

try 블록에서 작성한 코드가 예외 없이 정상 실행되면 catch 블록은 실행되지 않고 finally 블록 실행
try 블록에서 예외 발생 시 catch 블록 실행 후 finally 블록 실행
-> 예외 발생 여부와 관계없이 finally 블록은 항상 실행되며 생략 가능

## 예외 종류에 따른 처리
try 블록에서 다양한 종류의 예외가 발생할 수 있는데 다중 catch를 사용하면 발생하는 예외에 따라 예외 처리 코드를 다르게 작성할 수 있다.
```java
try {
    
} catch (NullPointerException e) {
    
} catch (IOException e) {
    
}
```
catch 블록이 여러 개라도 catch 블록은 하나만 실행된다.
try 블록에서 동시다발적으로 예외가 발생하지 않으며 하나의 예외가 발생하면 즉시 실행을 멈추고 해당 catch 블록으로 이동하기 때문이다.

처리해야할 예외 클래스들ㅇ리 상속 관계에 있을 때는 하위 클래스 catch 블록을 먼저 작성하고 상위 catch 블록을 나중에 작성해야한다.
catch 블록은 위에서부터 차례대로 검사 대상이 되기 때문에 하나의 상위 catch 블록에서 모두 예외를 처리하게 되기 때문이다.

```java
try {
    
} catch (IOException | NullPointerException e) {
    
}
```
두 개 이상의 예외를 하나의 catch 블록으로 동일하게 예외 처리하려면 위 코드처럼 예외 클래스를 `|` 기호로 연결하면 된다.

## 예외 떠넘기기
메서드 내부에서 예외 발생 시 try-catch 블록으로 예외를 처리하는 것이 기본이지만 throws 키워드를 사용하여 메서드를 호출한 곳으로 예외를 떠넘길 수 있다.

```java
public class ThrowsExample {
  public static void main(String[] args) {
    try {
      findClass();
    } catch(ClassNotFoundException e) {
      System.out.println("예외 처리:" + e.toString());
    }
  }

  public static void findClass() throws ClassNotFountException() {
    Class.forName("java.lang.String2);
  }
}
```
