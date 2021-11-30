### Enum

+ 서로 관련된 상수를 편리하게 선언하기 위한 것으로 상수를 여러개 정의할 때 사용한다.
+ 여러 상수를 정의한 후, 정의된 것 이외의 값은 허용하지 않는다.

#### 선언

```bash
enum 열거형이름 { 상수명1, 상수명2, 상수명3, ... }
```

- 열거형 필드의 이름은 상수이기 때문에 대문자로 표기한다.
- 기본적으로 0부터 시작하는 정수값이 연속적으로 부여된다.



#### Enum 을 사용하는 이유

+ Enum을 잘 사용하면 코드의 가독성을 높이고 논리적인 오류를 줄일 수 있다.

1. 상수는 변하지 않는다는 특징을 이용해 복잡한 값->단순한 값으로 치환해 사용할 수 있다.

   ```java
   public static void main(String[] args) {
       /*
        * 1 = banana
        * 2 = apple
        * 3 = lemon
        */
       int type = 1;
       switch(type) {
       case 1:
           System.out.println("banana");
           break;
       case 2:
           System.out.println("apple");
           break;
       case 3:
           System.out.println("lemon");
           break;
       }
   }
   ```

   + 문제점은 치환한 값에 대한 정보(주석)가 삭제될 경우 or 복잡한 코드로 주석을 찾기 어려워 질 경우 번호의 의미를 알 수 없다. 
   + 해결책으로 주석 삭제 후 변하지 않는 클래스 변수로 설정(final static)해 상수명 사용

2.  final static으로 설정해 주석 없이도 의미를 파악 할 수 있게 되었다.

   ```java
   private final static int BANANA = 1;
   private final static int APPLE = 2;
   private final static int LEMON = 3;
       
   public static void main(String[] args) {
       int type = BANANA;
       switch(type) {
       case 1:
           System.out.println("banana");
           break;
       case 2:
           System.out.println("apple");
           break;
       case 3:
           System.out.println("lemon");
           break;
       }
   }
   ```

   + 문제점은 같은 상수명을 갖는 다른 의미의 값이 존재 가능하고 그 경우 에러 발생할 수 있다.

   ```java
   private final static int BANANA = 1;
   private final static int APPLE = 2;        // 과일 사과 
   private final static int LEMON = 3;
       
   private final static int GOOGLE = 1;
   private final static int APPLE = 2;        // 회사 애플 
   private final static int MS = 3;
   ```

   + 해결책 중 하나로 Interface를 통한 상수명 구체화해 상수명의 중복을 피할 수 있다.

3. Interface로 상수명 구체화

   ```java
   interface FRUIT {
       final static int BANANA = 1;
       final static int APPLE = 2;        // 과일 사과 
       final static int LEMON = 3;
   }
    
   interface COMPANY {
       final static int GOOGLE = 1;
       final static int APPLE = 2;        // 회사 애플 
       final static int MS = 3;
   }
               .
               .
       int type = FRUIT.BANANA;
               .
               .
   
   ```

   + 문제점은 의미로 비교할 수 없는 상수 간의 비교가 가능하다. (비교를 하더라도 컴파일 에러가 발생하지 않는다.) 

   ```bash
   if (FRUIT.APPLE == COMPANY.APPLE) {
       System.out.println("과일 애플과 회사 애플은 같다.");
   }
   ```

   + 해결책 중 인스턴스 생성으로 데이터 타입을 구별해 비교 시 컴파일 에러 발생하도록 프로그래밍한다.

4. 인스턴스 생성

   ```java
   class Fruit {
       public final static Fruit APPLE = new Fruit();
       public final static Fruit BANANA = new Fruit();
       public final static Fruit LEMON = new Fruit();
   }
    
   class Company {
       public final static Company GOOGLE = new Company();
       public final static Company BANANA = new Company();
       public final static Company MS = new Company();
   ```

   + 문제점은 이렇게 노력해서 문제점을 해결해 놓았더니 switch문의 조건문에는 사용자 정의 클래스를 사용 할 수 없다.
   + 해결책으로 모든 조건 만족시켜며 switch문에서 사용 가능한 Enum 등장!