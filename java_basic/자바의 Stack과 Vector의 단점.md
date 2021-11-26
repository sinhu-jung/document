### 자바의 Stack과 Vector의 단점

#### Vector

+ Vector는 get과 set역할을 하는 모든 메서드에 synchronized 키워드가 붙어 있다.
+ 즉, Vector는 멀티 스레딩 동기화 기능을 제공한다. 한 번에 하나의 스레드만 Vector에 접근할 수 있다.
+ 메소드를 실행할 때마다 Lock을 걸고 푸는 오버헤드가 있다는 단점이 있다.



#### Stack

+ Stack은 Vector를 상속한다. 따라서 Vector의 단점을 그대로 물려 받는다. (이는 상속의 단점이다.)