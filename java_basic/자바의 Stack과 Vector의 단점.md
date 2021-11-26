### 자바의 Stack과 Vector의 단점

#### Vector

+ Vector는 get과 set역할을 하는 모든 메서드에 synchronized 키워드가 붙어 있다.
+ 즉, Vector는 멀티 스레딩 동기화 기능을 제공한다. 한 번에 하나의 스레드만 Vector에 접근할 수 있다.
- 단순히 Vector에 Iterator를 붙여 순차적으로 item들을 탐색하기만 해도 원소탐색 시마다 get() 메서드의 실행을 위해 계속 lock을 걸고 닫으므로 Iterator연산과정 전체에 1번만 걸어주면 될 locking에 쓸데없는 오버헤드가 엄청나게 발생
+ 메소드를 실행할 때마다 Lock을 걸고 푸는 오버헤드가 있다는 단점이 있다.



#### Stack

+ Stack은 Vector를 상속한다. 따라서 Vector의 단점을 그대로 물려 받는다. (이는 상속의 단점이다.)
