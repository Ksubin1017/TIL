# 기본 자료형
정수, 실수, 문자, 논리 리터럴을 저장하는 타입
연산을 위해 실제 값을 저장한다.

일반적인 로컬 연산, 성능이 중요한 반복 연산, null이 필요하지 않은 경우, 메모리 효율이 중요한 경우 사용한다.

## 특징
저장공간에 실제 자료 값을 가진다.
해당 값을 바로 사용할 수 있다.
산술 연산이 가능하다.
값 자체를 담는 공간이기 때문에 값이 없음을 의미하는 null 개념이 적용되지 않아 null을 저장할 수 없다.

# 참조 자료형
어떤 값이 저장되어 있는 주소를 값으로 저장하는 타입

컬렉션을 사용할 경우, null이 필요할 경우(Optional), 제네릭 타입 파라미터, API 응답 혹은 DTO일 경우

## 특징
산술연산이 불가능하다.
null로 초기화 할 수 있다.

#메모리
## 기본 매개변수
지역 변수 등 stack 영역에서 사용할 경우 stack에 실제 값을 저장하여 바로 사용할 수 있다.
```java
void change(int x) {
    x = 10;
}

int a = 5;
change(a);
System.out.println(a); // 5 출력
```
기본형 매개변수의 경우 값이 복사되어 메서드로 넘어가기 때문에 메서드 밖의 원본 값은 변경할 수 없다.
a의 값을 복사한 x만 값이 변경되고 메서드 밖 변수인 a는 그대로 5를 유지한다.

## 참조 매개변수
변수의 값을 변경할 수 있다.

```java
class MyClass {
    int value;
}

void change(MyClass obj) {
    obj.value = 10;
}

MyClass a = new MyClass();
a.value = 5;
change(a);
System.out.println(a.value); // 10 출력
```
참조 매겨변수의 경우 객체의 주소를 복사해서 전달하기 때문에 원본 값이 변경된다.

Boxing과 Unboxing
Boxing: 기본형 -> 참조형
Unboxing: 참조형 -> 기본형

java 5 이후부터 AutoBoxing과 AutoUnboxing을 지원하기 때문에 컴파일러가 박싱/언박싱을 자동으로 변환해준다.
