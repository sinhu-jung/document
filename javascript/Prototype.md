## Prototype

+ Class 라는 것은 Java, Python, C++ 등 객체지향 언어에서 빠질 수 없는 개념입니다. 

+ 하지만 자바스크립트도 객체지향 언어인데 자바스크립트에서는 Class라는 개념이 없습니다.

+ 대신 자바스크립트에서는 프로토타입 이라는 것이 존재 합니다.

  + 프로토타입은 기본적으로 상속 기능이 없습니다. 그래서 프로토타입 기반으로 상속을 흉내내도록 구현해 사용합니다.
  + 최근 ECMA6 표준에서는 Class 문법이 추가 되었지만 문법이 추가가 되었다는 것이지 자바스크립트가 클래스 기반으로 바뀐것은 아닙니다.

+ 프로토타입을 언제 쓰는지보면

  + 자바스크립트는 클래스는 없지만 함수와 new를 통해 클래스를 비스무리하게 흉내낼 수 있습니다.

    ```javascript
    function Person() {
      this.eyes = 2;
      this.nose = 1;
    }
    var kim  = new Person();
    var park = new Person();
    console.log(kim.eyes);  // => 2
    console.log(kim.nose);  // => 1
    console.log(park.eyes); // => 2
    console.log(park.nose); // => 1
    ```

  + kim과 park은 eyes와 nose를 공통적으로 가지고 있는데, 메모리에는 eyes와 nose가 두 개씩 총 4개 할당됩니다.

  + 객체를100개 만들면 200개의 변수가 메모리에 할당됩니다.

  + 이런 문제를 프로토타입으로 해결하는데 사용 됩니다.
  
    ```javascript
    function Person() {}
    Person.prototype.eyes = 2;
    Person.prototype.nose = 1;
    var kim  = new Person();
    var park = new Person():
    console.log(kim.eyes); // => 2
    ...
    ```
  
  + 즉 Person.prototype 이라는 빈 Object가 어딘가에 존재하고, Person 함수로부터 생성된 객체(kim, park)들은 어딘가에 존재하는 Object에 들어있는 값을 모두 갖다 쓸 수 있습니다.

#### Prototype Link와 Prototype Object

+ 자바스크립트에는 Prototype Link 와 Prototype Object라는 것이 존재합니다. 이 둘을 통틀어 Prototype 이라고 부릅니다.

##### Prototype Object

+ 객체는 언제나 함수(Function) 으로 생성 됩니다.

```javascript
function Person() {} // => 함수
var personObject = new Person(); // => 함수로 객체를 생성
```

+ personObject 객체는 Person이라는 함수로 생성된 객체입니다. 
+ 이렇듯 언제나 객체는 함수에서 시작됩니다.

```javascript
var obj = {};
```

+ 위의  코드에서 일반적인 객체생성도 함수랑 전혀 상관없는 코드 처럼 보이지만 아래 코드 처럼 함수와 관련이 많습니다.

```javascript
var obj = new Object();
```

+ Object는 자바스크립트에서 기본적으로 제공하는 함수이며 자바스크립트에서는 Function, Array 도 모두 함수로 정의 되어 있습니다.

+ 함수가 정의 될 때는 2가지 일이 동시에 일어납니다.

  1. 해당 함수에 Constructor(생성자) 자격 부여

     + Constructor 자격이  부여되면 new 키워드를 통해 객체를 만들 수 있게 됩니다.
     + 이것이 함수만 new 키워드를 사용할 수 있는 이유 입니다.
     + 따라서 Constructor 가 아니면 new 키워드를 사용할 수 없습니다.

  2. 해당 함수의 Prototype Object 생성 및 연결

     + 함수를 정의하면 함수만 생성되는 것이 아니라 Prototype Object도 같이 생성 됩니다.

     ![1_PZe_YnLftVZwT1dNs1Iu0A](https://user-images.githubusercontent.com/67888402/145132459-67833f37-3ee5-40a4-a3c9-75b92a59b575.png)

     + 생성된 함수는 prototype이라는 속성을 통해 Prototype Object에 접근할 수 있습니다.
     + Prototype Object는 일반적인 객체와 같으며 기본적인 속성으로 constructor와 proto를 가지고 있습니다.
     + constructor 는 Prototype Object와 같이 생성되었던 함수를 가리키고 있습니다.

     ```javascript
     function Person() {}
     Person.prototype.eyes = 2;
     Person.prototype.nose = 1;
     var kim  = new Person();
     var park = new Person():
     console.log(kim.eyes); // => 2
     ...
     ```

     + Prototype Object는 일반적인 객체이므로 속성을 마음대로 추가/삭제 할 수 있습니다. kim과 park은 Person 함수를 통해 생성되었으니 Person.prototype을 참조할 수 있게 됩니다.

##### Prototype Link

+ kim에는 eyes라는 속성이 없는데도 kim.eyes를 실행하면 2라는 값을 참조하는 것을 볼 수 있습니다. 위에서 설명했듯이 Prototype Object에 존재하는 eyes 속성을 참조한 것 입니다.
+ 바로 kim이 가지고 있는 딱 하나의 속성 proto 가 그것을 가능하게 해줍니다.
+ prototype 속성은 함수만 가지고 있던 것과는 달리 proto 속성은 모든 객체가 빠짐 없이 가지고 있는 속성 입니다.
+ proto는 객체가 생성 될 때 조상이였던 함수의 Prototype Object를 가리킵니다.  kim객체는 Person함수로부터 생성되었으니 Person 함수의 Prototype Object를 가리키고 있는 것입니다.

![1_jMTxqTYDZGhykJQoimmb0A](https://user-images.githubusercontent.com/67888402/145138231-07a23ac8-1c8d-4f96-81bf-2ffa11763f5f.png)

+ kim객체가 eyes를 직접 가지고 있지 않기 때문에 eyes 속성을 찾을 때 까지 상위 프로토타입을 탐색합니다. 최상위인 Object의 Prototype Object까지 도달했는데도 못찾았을 경우 undefined를 리턴합니다.
+ proto속성을 통해 상위 프로토타입과 연결되어있는 형태를 프로토타입 체인(Chain)이라고 합니다.

![1_mwPfPuTeiQiGoPmcAXB-Kg](https://user-images.githubusercontent.com/67888402/145138484-ab23758a-04b6-423f-ba6b-ec646e1097b1.png)

+ 이런 프로토타입 체인 구조 때문에 모든 객체는 Object의 자식이라고 불리고, Object Prototype Object에 있는 모든 속성을 사용할 수 있습니다. 
+ 한 가지 예를 들면 toString함수가 있겠습니다.

+  ES6에서 다음과 같이 proto is deprecated in ES6. 되었기 때문에 Object.getPrototypeOf 와 Object.setPrototypeOf를 사용하시면 되겠습니다.
