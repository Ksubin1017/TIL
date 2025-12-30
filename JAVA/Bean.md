# Java Bean
자바에서 재사용 가능한 소프트웨어 컴포넌트를 만들기 위한 규약
데이터를 담고 있고 외부에서 쉽게 접근할 수 있는 클래스이다.

## Java Bean 규약
- 기본 생성자를 갖는다.
- 클래스의 필드는 private로 외부에서 직접 접근 못하게 캡슐화 해야한다.
- 필드 값을 읽거나 수정하기 위한 getter, setter가 있어야 하며 public이어야한다.
- Serializable 인터페이스를 구현한다.

```java
import java.io.Serializable;

public class User implements Serializable {
    private String email;
    private String name;
    private int age;

    public User() {}

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```

## 사용 이유
여러 곳에서 재사용할 수 있으며 캡슐화로 필드 직접 접근이 아닌 getter, setter로 접근하여 유지보수가 쉽다.
Spring, JSP 등 프레임위크에서 데이터를 주고받을 때 편리하다.

## POJO와의 차이
POJO는 평범한 자바 객체로 특정 규약이나 인터페이스를 강제하지 않는다. Java Bean의 경우 Serializable과 기본 생성자를 강제하고 있다.
Java Bean은 POJO 규약 + 추가 규칙을 지킨 객체가 된다.
즉, 모든 Java Bean은 POJO지만, 모든 POJO가 Java Bean은 아니다.
