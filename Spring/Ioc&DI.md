# IoC(제어의 역전, Inversion Of Control)
다른 객체를 직접 생성하거나 제어하는 것이 아닌 외부에서 관리하는 객체를 가져와 사용하는 것
객체의 생명주기 관리를 외부(스프링 컨테이너)에 위임한다.

객체가 외부의 흐름에 의존하지 않기 때문에 변경 및 확장에 용이하다.
새로운 기능이 필요할 경우 기존 코드를 거의 수정하지 않고 외부에서 필요한 요소만 추가하면 되기에 변화하는 요구사항에 유연하게 대응할 수 있다.

```java
public class A {
  B b = new B();
}
```

위 코드에서는 클래스 B 객체를 사용하기 위해 클래스 A에서 객체를 직접 생성한다.
객체를 생성하고 사용하는 작업을 개발자가 직접 제어하는 코드이다.

```java
public class A {
  private B b;
}
```
제어의 역전을 적용하면 위 코드와 같이 변경된다. 클래스 B 객체를 직접 생성하는 것이 아닌 어딘가에서 받아와 사용한다.

# DI(의존성 주입, Dependency Injection)
어떤 클래스가 다른 클래스에 의존하는 것
객체가 필요한 의존성을 직접 생성하지 않고 외부에서 주입받는 방식으로 IoC의 구현 방법 중 하나이다.

코드의 결합도를 낮출 수 있기 때문에 테스트가 용이하고 외부에서 주입되는 객체를 변경함으로써 클래스의 기능을 쉽게 변경할 수 있다.

```java
public class A {
  @Autowired
  B b;
}
```
스프링 컨테이너가 B 객체를 만들어 클래스 A에 준 것과 같이 스프링 컨테이너에서 객채를 주입한다.
스프링의 경우 클래스 A에서 B 객체를 쓰고 싶은 경우 객체를 직접 생성하는 것이 아니라 스프링 컨테이너에서 객체를 주입받아 사용한다.

서비스 로직을 구성할 때 new를 통해 직접 객체를 생성하는 경우 기능이 변하게 되면 서비스 로직에서 객체를 직접 갈아끼워야한다.
의존성 주입을 사용하게 되면 서비스 로직의 변경은 최소화 하고 주입받은 객체만 수정하면 되기에 변경에 있어 더욱 용이해지는 것이다.

## 의존성 주입 방식
### 생성자 주입
```java
@Service
public class MemberService {
    private MemberRepository memberRepository;

    @Autowired
    public void setMemberRepository(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
}
```
생성자의 호출 시점에 1회 호출되는 것이 보장된다.
주입받은 객체가 변하지 않거나 반드시 객체의 주입이 필요한 경우 사용한다.
스프링 컨테이너가 객체를 빈 인스턴스로 생성할 때 생성자가 1회 호출되고 이후에 해당 빈의 의존관계는 변경되지 않는다.

### 필드 주입
```java
@Service
public class MemberService {

    @Autowired
    private MemberRepository memberRepository;
}
```
필드에 바로 의존관계를 주입하는 방법이다.
private로 선언된 필드에 주입하기 때문에 외부에서 접근할 수 없기 때문에 테스트 코드 작성 등 어려움이 발생한다.
특히 필드 주입은 의존성을 직접 주입하기 때문에 테스트 시 모의 객체를 쉽게 주입할 수 없어 테스트 작성이 어려워진다는 단점이 있다.
생성자의 경우 객체 생성이 완료됨과 동시에 의존성 주입도 완료되지만 필드 주입의 경우 객체 생성 이후 의존성을 주입받게 된다.
따라서 객체가 불완전상 상태인 시점이 존재하게 된다.

### 수정자(setter) 주입
```java
@Service
public class MemberService {
    private final MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
}
```
필드값을 변경하는 setter를 이용해 의존관계를 주입한다.
주입받는 객체가 변경될 가능성이 있는 경우에 사용한다.
