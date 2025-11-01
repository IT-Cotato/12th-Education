# 대본

## SOLID 관련 기본 내용

안녕하세요 이번 CS 교육을 맡은 12기 백엔드 강철웅입니다.  

이번 주 CS 교육의 주제는 SOLID입니다.

SOLID는 백엔드 파트 분들이라면 한 번쯤은 들어보셨을 텐데요,

먼저 교육 목표부터 확인하겠습니다. 
일단 SOLID가 무엇인지부터 알아보겠습니다.

그리고 각각의 원칙의 좋은 예시코드와 나쁜 예시 코드를 통해 자세히 알아보고 마지막으로 Solid 사용시 주의사항을 알아보갰습니다.

SOLID는 로버트 마틴이 제시한 객체지향 설계의 5가지 원칙입니다.

유지보수하기 쉽고 확장 가능한 소프트웨어를 만들기 위한 지침입니다.

각 원칙의 앞글자를 따서 SOLID라고 부르며,
실무에서 더 나은 코드를 작성하는 데 필수적인 개념들입니다.

한 가지 알아두면 좋은 게 있는데요,
이 5개 원칙이 독립적으로 보이지만
사실 서로 밀접하게 연결되어 있습니다.

하나의 원칙을 적용하면
자연스럽게 다른 원칙도 함께 적용되는 경우가 많아요.

---

그럼 SOLID에는 어떤 원칙들이 있는지 알아보겠습니다. 

S는 단일 책임 원칙, SRP
O는 개방-폐쇄 원칙, OCP
L은 리스코프 치환 원칙, LSP
I는 인터페이스 분리 원칙, ISP
D는 의존 역전 원칙, DIP

5가지 원칙입니다.

---

그럼 이 원칙들이 왜 중요할까요?

SOLID 원칙을 적용하면

첫째, 코드의 유지보수성이 향상됩니다. 변경이 쉬워지죠.

둘째, 확장 가능한 구조를 만들 수 있습니다.
새로운 기능 추가가 용이해집니다.

셋째, 안정성이 보장됩니다.
기존 코드를 건드리지 않고도 확장할 수 있어요.

넷째, 버그 발생 가능성이 감소합니다.

다섯째, 테스트하기가 쉬워집니다.

---

그럼 이제 각 원칙을 하나씩 자세히 알아보겠습니다.

---

## SRP

"첫 번째 원칙, 단일 책임 원칙인, SRP입니다.

SRP의 정의는 

'클래스는 하나의 책임만 가져야 하며,
단 하나의 변경 이유만을 가져야 한다'

SRP는 SOLID 원칙 중에서도 가장 기본이 되는 원칙입니다.
한 클래스가 너무 많은 일을 담당하면
코드가 복잡해지고 유지보수가 어려워집니다."

---

## SRP 나쁜 예시

```java
// SRP 위반: 너무 많은 책임을 가짐
public class Computer {
    public void startComputer() {
        System.out.println("부팅 중...");
        checkHardware();
        loadOS();
        connectNetwork();
        System.out.println("컴퓨터 준비 완료");
    }
    
    private void checkHardware() {
        System.out.println("하드웨어 점검");
    }
    
    private void loadOS() {
        System.out.println("운영체제 로딩");
    }
    
    private void connectNetwork() {
        System.out.println("네트워크 연결");
    }
}
```

먼저 나쁜 예시를 보겠습니다.

Computer 클래스가 있습니다.
startComputer 메서드를 보시면,

checkHardware로 하드웨어를 점검하고,
loadOS로 운영체제를 로딩하고,
connectNetwork로 네트워크를 연결합니다.

뭐가 문제일까요?

이 Computer 클래스가 하드웨어 점검, OS 로딩, 네트워크 연결 이렇게 세 가지 일을 다 하고 있습니다.

이렇게되면 예를 들어 하드웨어 점검 방식이 바뀌거나, OS 로딩 방식이 바뀌거나, 네트워크 연결 방식이 바뀔 때마다 Computer 클래스를 수정해야 합니다.

이는 SRP 위반입니다."

---

## SRP 개선된 코드

```java
// 각자 하나의 책임만 가짐
class Hardware {
    void check() {
        System.out.println("하드웨어 점검");
    }
}

class OS {
    void load() {
        System.out.println("운영체제 로딩");
    }
}

class Network {
    void connect() {
        System.out.println("네트워크 연결");
    }
}

public class Computer {
    private final Hardware hardware = new Hardware();
    private final OS os = new OS();
    private final Network network = new Network();
    
    public void startComputer() {
        hardware.check();
        os.load();
        network.connect();
    }
}
```

개선된 코드를 보겠습니다.

Hardware, OS, Network를
각각 별도 클래스로 분리했습니다.

Hardware 클래스는 check 메서드만 가지고 있습니다.
하드웨어 점검만 담당하죠.

OS 클래스는 load 메서드만 가지고 있습니다.
운영체제 로딩만 담당합니다.

Network 클래스는 connect 메서드만 가지고 있습니다.
네트워크 연결만 담당하고요.

그리고 Computer 클래스는,
이 세 개의 클래스를 가지고 있으면서
startComputer에서 순서대로 호출만 합니다.

이렇게하면 각 클래스는 명확히 하나의 책임만 가집니다.

네트워크 연결 방식을 바꿔도
Hardware나 OS 클래스는 전혀 영향받지 않습니다.

각 기능이 독립적으로 관리됩니다.

---

## OCP

두 번째 원칙, 개방-폐쇄 원칙, OCP입니다.

'확장에는 열려 있고, 수정에는 닫혀 있어야 한다'

쉽게 말하면, 새로운 기능을 추가할 때 기존 코드를 건드리지 말라는 겁니다.

이는 소프트웨어의 확장성과 안정성을
동시에 보장하는 핵심적인 개념입니다.

---

## OCP 나쁜 예시

```java
// OCP 위반: 새로운 연산 추가 시 기존 코드 수정 필요
class Calculator {
    public double calculate(String operation, double a, double b) {
        if (operation.equals("add")) {
            return a + b;
        } else if (operation.equals("multiply")) {
            return a * b;
        }
        // 새로운 연산을 추가하려면 이 메서드를 수정해야 함
        return 0;
    }
}
```

나쁜 예시를 볼게요.
계산기를 만든다고 생각해봅시다.

Calculator 클래스에 calculate 메서드가 있습니다.

문자열로 "add"를 받으면 a + b로 덧셈을 하고,
"multiply"를 받으면 a * b로 곱셈을 합니다.

여기서 문제가 뭘까요?

나눗셈을 추가하고 싶으면 어떻게 해야 할까요?

이 calculate 메서드를 열어서
else if를 추가해야 합니다.

뺄셈을 추가하고 싶으면?
또 이 메서드를 수정해야 하죠.

기능을 추가할 때마다
기존 코드를 계속 수정해야 합니다.

그리고 if-else가 계속 늘어나게 되고,
기존 코드를 건드리면
기존 기능에 버그가 생길 위험도 있습니다.

이게 OCP 위반입니다.

---

## OCP 개선된 코드

```java
// 인터페이스로 확장 가능하게 설계
interface Operation {
    double execute(double a, double b);
}

class Addition implements Operation {
    public double execute(double a, double b) {
        return a + b;
    }
}

class Multiplication implements Operation {
    public double execute(double a, double b) {
        return a * b;
    }
}

// 새로운 연산 추가 시 기존 코드 수정 없이 확장 가능
class Division implements Operation {
    public double execute(double a, double b) {
        if (b != 0) {
            return a / b;
        }
        throw new IllegalArgumentException("0으로 나눌 수 없습니다");
    }
}

class Calculator {
    public double calculate(Operation operation, double a, double b) {
        return operation.execute(a, b);
    }
}
```

Operation이라는 인터페이스를 만듭니다.
이건 '연산'이라는 공통 규약입니다.

그리고 Addition, Multiplication, Division을
각각 별도 클래스로 만듭니다.

Addition 클래스는 execute에서 a + b를 반환하고,
Multiplication 클래스는 a * b를 반환하고,
Division 클래스는 b가 0이 아니면 a / b를 반환합니다.

이렇게 하면 새로운 연산을 추가할 때
Calculator 클래스는 하나도도 안 건드린다는 겁니다

뺄셈, 제곱을 추가하고 싶으면
Subtraction, Power 클래스만 새로 만들면 끝나고
Calculator는 그대로 둬도 됩니다.

기존 코드는 전혀 수정하지 않고
새로운 기능만 추가합니다.

---

## LSP

세 번째 원칙, 리스코프 치환 원칙, LSP입니다.

'자식 클래스는 언제나 부모 클래스를 대체할 수 있어야 한다'

LSP는 상속을 올바르게 사용하기 위한 원칙입니다.

부모 클래스 타입의 객체를 자식 클래스 타입의 객체로 치환해도
프로그램이 정상적으로 동작해야 한다는 거죠.

---

## LSP 나쁜 예시

```java
// LSP 위반 예시
class Bird {
    public void fly() {
        System.out.println("날아간다");
    }
}

class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("타조는 날 수 없다");
    }
}

// 문제 상황
public class Zoo {
    public void makeBirdFly(Bird bird) {
        bird.fly(); // Bird 타입이면 당연히 날 수 있다고 가정
    }
}

Zoo zoo = new Zoo();
zoo.makeBirdFly(new Ostrich()); // 💥 예외 발생! LSP 위반
```

동물원에 새들을 날리는 프로그램이 있다고 생각해봅시다.

Bird 클래스가 있고, fly 메서드가 있습니다.
"날아간다"를 출력하죠.

그리고 타조, Ostrich 클래스가 있습니다.
타조도 새니까 Bird를 상속받았습니다.

근데 문제가 뭘까요?

타조는 날 수 없잖아요?

그래서 fly 메서드를 오버라이드해서
예외를 던집니다.
"타조는 날 수 없다"

이제 Zoo 클래스를 보시면,
makeBirdFly 메서드가 있습니다.

Bird 타입을 받으니까
"새는 날 수 있겠지"라고 당연히 가정하고
bird.fly()를 호출합니다.

그럼 어떻게 될까요?

타조를 넣으면? 예외 발생하게 됩니다.

이게 바로 LSP 위반입니다.

Bird 타입 자리에 Ostrich를 넣으니까 예외가 터진 거죠.

부모 클래스를 자식 클래스로 대체할 수 없는 겁니다."

---

## LSP 개선된 코드

```java
// 날 수 있는 능력을 인터페이스로 분리
interface Flyable {
    void fly();
}

// 날 수 있는 새들
class Sparrow implements Flyable {
    public void fly() {
        System.out.println("참새가 날아간다");
    }
}

class Eagle implements Flyable {
    public void fly() {
        System.out.println("독수리가 날아간다");
    }
}

class Pigeon implements Flyable {
    public void fly() {
        System.out.println("비둘기가 날아간다");
    }
}

// 날 수 없는 새들
class Ostrich {
    public void run() {
        System.out.println("타조가 달린다");
    }
}

class Penguin {
    public void swim() {
        System.out.println("펭귄이 헤엄친다");
    }
}

// 동물원
public class Zoo {
    public void makeFly(Flyable bird) {
        bird.fly(); // Flyable이면 100% 날 수 있음 보장
    }
    
    public static void main(String[] args) {
        Zoo zoo = new Zoo();
        
        // 날 수 있는 새들 - 모두 정상 작동 ✅
        zoo.makeFly(new Sparrow());  // "참새가 날아간다"
        zoo.makeFly(new Eagle());    // "독수리가 날아간다"
        zoo.makeFly(new Pigeon());   // "비둘기가 날아간다"
        
        // 날 수 없는 새들 - 타입이 안 맞아서 넣을 수 없음
        // zoo.makeFly(new Ostrich());  // ❌ 컴파일 에러!
        // zoo.makeFly(new Penguin());  // ❌ 컴파일 에러!
        
        // 날 수 없는 새들은 각자의 메서드 사용
        Ostrich ostrich = new Ostrich();
        ostrich.run();  // "타조가 달린다"
        
        Penguin penguin = new Penguin();
        penguin.swim(); // "펭귄이 헤엄친다"
    }
}
```

```

"개선된 코드를 볼까요?
해결 방법은 간단합니다.

날 수 있는 새와 날 수 없는 새를
애초에 다른 타입으로 만드는 겁니다.

Flyable이라는 인터페이스를 만듭니다.
'날 수 있는 것'을 나타내는 인터페이스죠.

그리고 날 수 있는 새들,
Sparrow, Eagle, Pigeon이 모두 Flyable을 구현합니다.

참새는 "참새가 날아간다",
독수리는 "독수리가 날아간다",
비둘기는 "비둘기가 날아간다"를 출력합니다.

반면에 타조와 펭귄은?
이들은 아예 Flyable이 아닙니다.
각자 달리기, 헤엄치기만 합니다.

---

이제 Zoo 클래스를 보시면,
makeFly 메서드가 Flyable 타입을 받습니다.

makeFly는 부모 타입인 Flyable을 받지만,
실제로 사용할 때는 자식인 Sparrow, Eagle, Pigeon을 넣습니다.

참새, 독수리, 비둘기를 넣으면? 모두 정상 작동하게됩니다.
부모 타입 자리에 자식을 넣어도
예외 없이 모두 잘 동작합니다.

이게 바로 LSP입니다!

Flyable 타입 자리에
어떤 Flyable 구현체를 넣어도
100% 안전하게 동작한다는 게 보장되는 거죠.

---

반대로 타조나 펭귄은?
Flyable이 아니니까 makeFly에 넣을 수가 없습니다.
컴파일 에러가 나서 미리 방지되는 거죠.

이전 코드에서는 Bird 자리에 Ostrich를 넣으면 예외가 터졌지만,
이제는 타입 자체가 달라서 잘못 사용할 수가 없게 됐습니다."

여기가 중요합니다!

makeFly는 부모 타입인 Flyable을 받지만,
실제로 사용할 때는 자식인 Sparrow, Eagle, Pigeon을 넣습니다.

부모 타입 자리에 자식을 넣어도
예외 없이 모두 잘 동작합니다.

이것이 LSP입니다. 

---

## ISP

네 번째 원칙, 인터페이스 분리 원칙, ISP입니다.

특정 클라이언트에 맞는 인터페이스를 제공해야 하며,
불필요한 메서드가 포함된 거대한 인터페이스를 만들지 않아야 한다

ISP는 클라이언트가 자신이 사용하지 않는 메서드에 의존하게 되는 것을 방지하는 원칙입니다.

거대한 인터페이스보다는
구체적이고 작은 인터페이스들이 낫다는 겁니다.

---

## ISP 나쁜 예시

```java
// ISP 위반: 너무 많은 기능이 한 인터페이스에
interface Machine {
    void print();
    void scan();
    void fax();
}

class SimplePrinter implements Machine {
    public void print() { 
        System.out.println("문서를 인쇄합니다");
    }
    
    public void scan() { 
        // 사용하지 않는 기능이지만 구현해야 함
        throw new UnsupportedOperationException("스캔 기능 없음");
    }
    
    public void fax() { 
        // 사용하지 않는 기능이지만 구현해야 함
        throw new UnsupportedOperationException("팩스 기능 없음");
    }
}
```

나쁜 예시를 볼게요.
프린터 인터페이스가 있습니다.

Machine 인터페이스를 보시면, print, scan, fax 메서드가 모두 들어있습니다.
인쇄, 스캔, 팩스 기능이 다 있는 거죠.

이제 SimplePrinter 클래스를 보겠습니다.
이건 단순 프린터입니다.

Machine 인터페이스를 구현하니까
print, scan, fax를 모두 구현해야 합니다.

print는 괜찮습니다. 프린터는 인쇄 기능이 필요합니다.

하지만 단순 프린터는 스캔 기능도 없고, 팩스 기능도 없습니다.

그래서 "스캔 기능 없음", "팩스 기능 없음"이라는 예외를 던집니다.

여기서 문제는 단순 프린터는 인쇄 기능만 필요한데, 스캔과 팩스 기능까지 구현해야 합니다.

불필요한 의존성이 생기는 겁니다.

사용하지도 않는 메서드 때문에
예외 처리 코드까지 작성해야 하고요.

이게 ISP 위반입니다."

---

## ISP 개선된 코드

```java
// 기능별로 인터페이스 분리
interface Printable {
    void print();
}

interface Scannable {
    void scan();
}

interface Faxable {
    void fax();
}

class SimplePrinter implements Printable {
    public void print() {
        System.out.println("문서를 인쇄합니다");
    }
}

class MultiFunctionPrinter implements Printable, Scannable, Faxable {
    public void print() {
        System.out.println("문서를 인쇄합니다");
    }
    
    public void scan() {
        System.out.println("문서를 스캔합니다");
    }
    
    public void fax() {
        System.out.println("팩스를 전송합니다");
    }
}
```

"개선된 코드를 볼까요?
기능별로 인터페이스를 분리했습니다.

Printable 인터페이스는 print만,
Scannable 인터페이스는 scan만,
Faxable 인터페이스는 fax만 가지고 있습니다.

이제 SimplePrinter를 보시면,
Printable만 구현합니다.

print 메서드만 구현하면 끝입니다.
"문서를 인쇄합니다"

스캔이나 팩스는?
구현할 필요가 없습니다!
애초에 Printable에 그런 메서드가 없으니까요.

이제 MultiFunctionPrinter를 보겠습니다.
이건 다기능 프린터죠.

이 클래스는 Printable, Scannable, Faxable을
모두 구현합니다.

print, scan, fax를 모두 구현하는 거죠.

여기가 ISP의 핵심입니다!

SimplePrinter는 자신이 실제로 사용하는 기능,
즉 Printable에만 의존합니다.

MultiFunctionPrinter는 필요한 모든 기능,
Printable, Scannable, Faxable 모두에 의존하고요.

각 클래스가 자신이 실제로 사용하는 기능에만 의존하게 된 겁니다.
불필요한 예외 처리도 사라졌고, 코드가 훨씬 깔끔해졌습니다.

---

## DIP

마지막 원칙, 의존 역전 원칙, DIP입니다.

'상위 모듈이 하위 모듈에 직접 의존하지 않고,
추상화를 통해 의존성을 줄여야 한다'

DIP는 의존성의 방향을 역전시켜
더 유연한 설계를 만드는 원칙입니다.

구체적인 구현체에 의존하는 것이 아니라
추상화, 즉 인터페이스에 의존해야 한다는 겁니다.

---

## DIP 나쁜 예시

```java
// DIP 위반: 구체적인 클래스에 직접 의존
class MySQLDatabase {
    public void connect() {
        System.out.println("MySQL에 연결");
    }
}

class DataService {
    private final MySQLDatabase database; // 구체적인 클래스에 직접 의존
    
    public DataService() {
        this.database = new MySQLDatabase(); // 강한 결합!
    }
    
    public void use() {
        database.connect();
    }
}
```

나쁜 예시를 볼게요.
MySQLDatabase 클래스가 있습니다.
connect 메서드로 MySQL에 연결하는 거죠.

이제 DataService 클래스를 보겠습니다.

여기를 보시면,
private final MySQLDatabase database

MySQLDatabase를 직접 사용하고 있습니다.

그리고 생성자에서,
new MySQLDatabase()로 직접 생성합니다.

문제가 뭘까요?

첫째, 데이터베이스를 PostgreSQL로 바꾸고 싶으면?

DataService 코드를 열어서
MySQLDatabase를 PostgreSQLDatabase로
수정해야 합니다.

둘째, 테스트하려면?

진짜 MySQL 서버가 꼭 필요합니다.
가짜 데이터베이스로 테스트할 수가 없어요.

셋째, 새로운 DB를 추가할 때마다
DataService를 계속 수정해야 합니다.

DataService가 MySQL에 강하게 결합되어 있는 거죠.

이게 DIP 위반입니다.

---

## DIP 개선된 코드

```java
// DIP 준수: 추상화에 의존
interface Database {
    void connect();
}

class MySQLDatabase implements Database {
    public void connect() {
        System.out.println("MySQL에 연결");
    }
}

class PostgreSQLDatabase implements Database {
    public void connect() {
        System.out.println("PostgreSQL에 연결");
    }
}

class DataService {
    private final Database database; // 인터페이스에 의존
    
    // 의존성 주입 (Dependency Injection)
    public DataService(Database database) {
        this.database = database;
    }
    
    public void use() {
        database.connect();
    }
}
```

Database 인터페이스를 만들었습니다. 이렇게 해서 데이터베이스'라는 개념만 정의합니다.

이제 MySQLDatabase와 PostgreSQLDatabase가
각각 Database 인터페이스를 구현합니다.

MySQL은 "MySQL에 연결",
PostgreSQL은 "PostgreSQL에 연결"을 출력하죠.

이제 DataService를 보시면,
private final Database database

이제 Database 인터페이스 타입을 사용합니다.

MySQL인지 PostgreSQL인지 몰라도 됩니다.
그냥 Database면 괜찮은 거죠.

그리고 생성자를 보시면,
public DataService(Database database)

외부에서 Database를 받아옵니다.
직접 생성하지 않아요.

이게 바로 의존성 주입, Dependency Injection입니다.

---

## 주의사항

지금까지 SOLID 5가지 원칙을 알아봤습니다.

SOLID 원칙을 적용할 때 주의할 점이 있습니다.

바로 과도한 적용을 주의해야 한다는 겁니다.

모든 상황에 무조건 적용할 필요는 없어요.

프로젝트의 규모와 복잡도를 고려해야 합니다.

간단한 코드를 불필요하게 복잡하게 만들 필요는 없죠.

"완벽한 설계"에 집착할 필요 없습니다.

---

## 언제 적용할까?

"그럼 언제 SOLID 원칙을 적용해야 할까요?

첫째, 코드가 자주 변경되는 부분입니다.
이런 부분은 SOLID를 적용하면
변경이 훨씬 쉬워집니다.

둘째, 여러 곳에서 재사용되는 부분입니다.
재사용성을 높이려면 SOLID가 필요하죠.

셋째, 테스트가 필요한 핵심 로직입니다.
SOLID를 적용하면 테스트하기 쉬워집니다.

반대로 언제 적용하지 말아야 할까요?

한 번만 사용되는 단순한 코드,
변경 가능성이 거의 없는 부분은
굳이 복잡하게 만들 필요가 없습니다.

퀴즈 사이트 오류 이슈로 참고할 사진이 필요한 경우 공지방에 올릴 예정이니 공지방 카톡도 함께 봐주세요

9번 후 킹캉 진출자 확인하기