### String vs StringBuffer/StringBuilder

+ String과 StringBuffer/StringBuilder의 가장 큰 차이점은 String은 불변의 속성을 가짐
+ 즉 String 객체는 한번 생성되면 할당된 공간이 변하지 않지만 StringBuffer나 StringBuilder의 경우 객체의 공간이 부족해지는 경우 버퍼의 크기를 유연하게 늘려줌

#### String

``` bash
String str = "hello"
str = str + "world"
```

위의 예제를 보면 기존에 "hello" 값이 들어가있던 String 클래스의 참조변수 str이 "hello world"라는 값을 가지고 있는 새로운 메모리영역을 가리키게 변경되고 처음 선언했던 "hello"로 값이 할당되어 있던 메모리 영역은 Garbage로 남아있다가 GC(garbage collection)에 의해 사라지게 되는 것이며 String 클래스는 불변하기 때문에 문자열을 수정하는 시점에 새로운 String 인스턴스가 생성된 것임

![캡처](https://user-images.githubusercontent.com/67888402/143513881-d9321307-a4b9-44a4-981f-477c5ec6781a.PNG)

+ String의 장점은 String 클래스는 크기가 고정되어 있으므로 단순하게 읽는 조회 연산에서는 StringBuffer나 StringBuilder클래스보다 빠르게 읽을 수 있는 장점이 있음
+ StringBuffer나 StringBuilder을 생성할 경우 buffer의 크기를 초기에 설정해줘야하는데 이러한 동작으로 인해 String객체보다 생성 속도가 많이 느려지게 되고 StringBuffer나 StringBuilder에서 문자열 수정을 할 경우에도 마찬가지로 버퍼의 크기를 늘리고 줄이고 명칭을 변경해야하는 내부적인 연산이 필요하므로 많은 양의 문자열 수정이 아니라면 String객체를 사용하는것이 오히려 나을 수 있음

#### StringBuffer/StringBuilder

+ String 과는 반대로 StringBuffer/StringBuilder 는 가변성 가지기 때문에 .append() .delete() 등의 API를 이용하여 **동일 객체내에서 문자열을 변경**하는 것이 가능하며 **문자열의 추가,수정,삭제가 빈번하게 발생할 경우**라면 String 클래스가 아닌 **StringBuffer/StringBuilder를 사용** 해야함

```b
StringBuffer sb= new StringBuffer("hello"); 
sb.append(" world");
```

![캡처](https://user-images.githubusercontent.com/67888402/143514110-4b848143-d8e4-40f0-8de9-af15c2603cb9.PNG)

#### StringBuffer vs StringBuilder

+ StringBuffer와 StringBuilder의 차이점은 StringBuffer는 동기화를 지원 하여 멀티 쓰레드 환경에서 안전하게 사용이 가능하다. String도 불변성을 가지기 때문에 마찬가지로 멀티쓰레드 환경에서 안정성을 가지고 있음
+ 반대로 StringBuilder는 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에서 사용하는 것은 적합하지 않지만 동기화를 고려 하지 않는 만큼 단일 쓰레드에서의 성능은 StringBuffer 보다 뛰어남



#### 정리

**String**          : 문자열 연산이 적고 멀티쓰레드 환경일 경우

**StringBuffer**   : 문자열 연산이 많고 멀티쓰레드 환경일 경우

**StringBuilder**  : 문자열 연산이 많고 단일쓰레드이거나 동기화를 고려하지 않아도 되는 경우 
