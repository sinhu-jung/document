### String vs StringBuffer/StringBuilder

+ String과 StringBuffer/StringBuilder의 가장 큰 차이점은 String은 불변의 속성을 가짐

#### String

``` bash
String str = "hello"
str = str + "world"
```

위의 예제를 보면 기존에 "hello" 값이 들어가있던 String 클래스의 참조변수 str이 "hello world"라는 값을 가지고 있는 새로운 메모리영역을 가리키게 변경되고 처음 선언했던 "hello"로 값이 할당되어 있던 메모리 영역은 Garbage로 남아있다가 GC(garbage collection)에 의해 사라지게 되는 것이며 String 클래스는 불변하기 때문에 문자열을 수정하는 시점에 새로운 String 인스턴스가 생성된 것임

![캡처](https://user-images.githubusercontent.com/67888402/143513881-d9321307-a4b9-44a4-981f-477c5ec6781a.PNG)

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