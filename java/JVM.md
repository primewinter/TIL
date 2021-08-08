### JVM이란

자바를 실행하기 위한 가상 컴퓨터로, 메모리 관리를 수행하고 JAVA와 OS사이에서 중개자 역할을 수행해서 JAVA가 OS로부터 독립적이게 만드는 역할을 합니다.

### **JVM(Java Virtual Machine) 특징**

- 자바를 실행하기 위한 가상 컴퓨터
- JAVA와 OS 사이에서 중개자 역할을 수행하여 JAVA가 OS에 독립적이게 한다.
- 메모리관리와 GC를 수행한다

### Java의 실행방식

- 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어 자바 바이트코드(.class)로 변환시킵니다.
- Class Loader를 통해 class 파일들을 JVM으로 로딩합니다.
- 로딩된 class파일들은 Execution engine을 통해 해석됩니다.
- 해석된 바이트코드는 Runtime Data Areas 에 배치되어 실질적인 수행이 이루어집니다.

### **Garbage Collector**

자바에서는 메모리를 가비지 컬렉터(GC)를 통하여 관리하기 때문에 개발자는 메모리를 처리하기 위한 로직을 만들 필요도 없고, 구현해서도 안된다고 알고 있습니다.

JVM의 메모리는 크게 

- 클래스 영역
- 스택 영역
- **힙 영역**
- 네이티브 메소드 스택 영역

으로 나뉘고 있는데 GC는 힙 영역을 다루게 됩니다.

메모리를 할당을 하고, 사용중인 메모리와 사용하지 않는 메모리를 인식하여 처리를 합니다.

### JVM 힙 영역

은 다시 Young, Old, Perm 세영역으로 나뉩니다.

**YOUNG GENERATION** **[       Eden      | Survivor | Survivor |     Virtual     ]**

**OLD GENERATION [            Old           | Virtual ]**

**PERM GENERATION [            Perm            | Virtual ]**

- **Perm 영역**은 거의 사용되지 않고, 클래스와 메소드 정보와 같이 자바언어 레벨에서는 사용되지 않습니다. (application을 실행할때 클래스의 메타 데이터를 저장하는 영역)
- **Young 영역**은
    - **Eden** 과
    - **두개의 Survivor**

영역으로 나뉩니다. (새로 생성한 객체를 저장하는 영역)

일단 메모리에 객체가 생성되면, Eden 영역에 객체가 지정됩니다.  Eden 영역에 데이터가 어느 정도 쌓이면, 이 영역에 있던 객체가 어디론가 옮겨지거나 삭제됩니다. 이 때 옮겨가는 위치가 survivor 영역입니다. 두개의 Survivor 영역 사이에 우선 순위가 있는 것은 아닙니다. 하지만, 이 두 개의 영역 중 한 영역은 반드시 비어 있어야 합니다. 그 비어있는 영역에 Eden 영역에 있던 객체가 할당됩니다.

Eden에서 survivor 둘 중 하나의 영역으로 할당 되고, 할당된 Survivor 영역이 차면, GC가 되면서 Eden 영역에 있는 객체와 꽉 찬 Survivor 영역에 있는 객체가 비어 있는 Survivor 영역으로 이동합니다. 그러다가 더 큰 객체가 생성되거나, 더 이상 Young 영역에 공간이 남지 않으면 객체들은 Old 영역으로 이동하게 됩니다.

- **마이너 GC:** Young 영역에서 발생하는 GC
- **메이저 GC:** Old 영역이나 Perm 영역에서 발생하는 GC
