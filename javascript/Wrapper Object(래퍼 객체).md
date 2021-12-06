## Wrapper Object(래퍼 객체)

+ 래퍼 객체란 이름처럼 원시 타입의 값을 감싸는 형태의 객체이다.
+ 래퍼 객체에는 Number, String, Boolean, Symbol 이 제공 된다.

### String()

+ 인자를 문자열로 바꿔주는 함수이다.

  ```javascript
  String(1337); // "1337"
  String(null); // "null"
  String(true); // "true"
  ```

+ String 함수에 new 키워드를 붙여서 사용하게 되면  생성자로 동작을 하는데 new String('dog')와 같이 실행 시키면

  ```javascript
  {
  	0: "d",
  	1: "o",
  	2: "g",
  	length : 3
  }
  ```

  + 위와 같이 문자열을 포장하는 객체를 만들어서 리턴해준다.

### 오토박싱

``` javascript
const pet = new String("dog");
pet.constructor === String; // true
String("dog").constructor === String; // true
```

+ 첫 번째 줄을 보면
  1. String함수를 생성자로 호출했고 "dog"을 인자로 전달했다.
  2. String 래퍼 객체가 생성되었다.
  3. 이 객체는 [[prototype]] 링크로 String()함수의 프로토타입 객체를 가리킨다.
  4. pet이라는 참조변수는 이 객체를 가리키고 있다.

+ 두 번째 줄을 보면
  1. pet에는 constructor 속성이 없다.
  2. 프로토타입 체이닝이 일어나서 프로토타입의 constructor가 가리키는 것을 확인 해보니 String() 함수이다.
  3. 그렇기 때문에 true가 나온다.
+ 마지막 줄을 보면
  1. String("dog")이 실행되면 "dog" 이라는 원시타입 문자열이 리턴된다.
  2. "dog".constructor === String 문장이 실행되는데, 여기서 어떻게 원시타입이 constructor라는 속성을 가지는지 의문이 생긴다.
  3. JS 인터프리터가 이 원시타입을 래퍼객체로 자동으로 감싸주기 때문에 이런일이 가능한것이다.
  4. 래퍼객체로 변환된 "dog"는 위와 같은 과정이 일어나고 마찬가지로 true가 리턴된다.
  5. 래퍼 객체를 모두 사용하고 난 뒤 이 래퍼객체를 지워버린다.(gc가 처리해버림)

+ 이 세번째 줄에서 원시타입을 래퍼 객체로 자동 변환 해주는 작업을 오토박싱이라 한다.

#### 오토박싱 - 2

```javascript
const foo = "bar";
foo.length; // 3
foo === "bar"; // true
```

+ 여기서 두 번째 줄을 살펴보면
  + foo는 원시타입이다. 그런데 length라는 프로퍼티에 접근하고 있는데도 오류가 안난다.
  + JS가 foo를 감싸는 래퍼객체를 만들고나서 length 프로퍼티를 사용한다.
  + 다 사용하고 나서 2번째 줄이 끝나게 되면 래퍼객체를 지운다.