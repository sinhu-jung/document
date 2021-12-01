### JavaScript 기본형

+ Type을 알고 싶으면 typeof를 사용하면 알수있다.

#### Primative Type

+ 객체가 아닌 데이터 유형을 말한다.
  + Number
  + String
  + Boolean
  + Symbol(ES6에 추가, 객체 속성을 만드는 데이터 타입)
  + null
  + undefined

+ 기본형 데이터는 값을 그대로 할당하는 것이다. 메모리상에 고정된 크기로 저장되며 원시 데이터 값 자체를 보관하므로, 불변적이다.
+ 기본적으로 같은 데이터는 하나의 메모리를 사용한다.(재사용)
+ 원시 타입 데이터는 각 변수간에 데이터를 복사할 경우, **데이터 값**이 복사되기 때문에 기존의 데이터에 영향이 가지 않는다.



#### Reference Type

+ 참조 타입은 변수에 할당할때 값이 아닌 데이터의 주소를 저장한다.
+ 원시 자료형이 아닌 모든 것은 참조 자료형. 배열([])과 객체({}), 함수(function(){})가 대표적이다.
  + Object
  + Array
    + const 로 선언된 변수 배열에 Array.push를 적용할 수 있는 이유는 배열은 참조 타입이기 때문에 데이터의 주소를 대입할 수 있기 때문이다.
  + Function RegExp
    + 문자열에 나타나는 특정 문자조합과 대응시키기 위해 사용되는 패턴이다.
  + Map
  + else...
+ 참조 자료형은 기존에 고정된 크기의 보관함이 아니라, 동적으로 크기가 변하는 특별한 보관함을 사용할 수 있습니다.



#### null 과 undefined

+ JavaScript에는 '없음'를 나타내는 값이 두 개 있는데, 바로 `null`와 `undefined`입니다.

+ null은 존재 하지않음 이라는 값

+ undefined는 정의 되지않음 이라는 값

  + JavaScript는 값이 대입되지 않은 변수 혹은 속성을 사용하려고 하면 `undefined`를 반환합니다.

  ``` javascript
  let foo;
  foo // undefined
  
  const obj = {};
  obj.prop; // undefined
  ```

  + `null`은 '객체가 없음'을 나타냅니다. 실제로 `typeof` 연산을 해보면 아래와 같은 값을 반환합니다.

  ```javascript
  typeof null // 'object'
  typeof undefined // 'undefined'
  ```

  + 그렇다면 개발자의 입장에서 **'없음'**을 저장하기 위해 둘 중 어떤 것을 써야 할까요? `undefined`를 쓴다고 가정해보면, 아래와 같은 코드는 그 의미가 불분명해집니다.

  ```javascript
  let foo; // 값을 대입한 적 없음
  let bar = undefined; // 값을 대입함
  foo; // undefined
  bar; // undefined (??)
  let obj1 = {}; // 속성을 지정하지 않음
  let obj2 = {prop: undefined}; // 속성을 지정함
  obj1.prop; // undefined
  obj2.prop; // undefined (??)
  ```

  + 비록 `undefined`가 '없음'을 나타내는 값일지라도, 대입한 적 없는 변수 혹은 속성과, 명시적으로 '없음'을 나타내는 경우를 **구분**을 할 수 있어야 코드의 의미가 명확해 질 것입니다. **프로그래머의 입장에서 명시적으로 부재를 나타내고 싶다면 항상 null을 사용**하는 것이 좋습니다.
  + 다만, 객체를 사용할 때 어떤 속성의 부재를 `null`을 통해서 나타내는 쪽보다는, 그냥 그 속성을 정의하지 않는 방식이 간편하므로 더 널리 사용됩니다.

  ```javascript
  // 이렇게 하는 경우는 많지 않습니다.
  {
    name: 'Seungha',
    address: null
  }
  
  // 그냥 이렇게 하는 경우가 많습니다.
  {
    name: 'Seungha'
  }
  
  // 어쨌든 이렇게 하지는 말아주세요.
  {
    name: 'Seungha',
    address: undefined
  }
  ```



#### Symbol

+ 심볼은 변경 불가능한 원시 타입의 값이며, 다른 값과 중복되지 않는 고유한 값이다. 
+ 심볼 값은 충돌 위험이 없는 오브젝트의 유일한 프로퍼티 키를 만들기 위해서 사용할 수 있다. 하위호환성을 유지하면서 표준을 확장한다든지, 고유한 상수값을 만드는 데 사용할 수 있다.

+ Symbol 값은 Symbol 함수를 호출하여 생성한다. 심볼 값은 자바스크립트 런타임 환경에서 Symbol 함수에 의해 동적으로 생성되며 다른 값과 중복되지 않는 고유한 값이다. 생성된 심볼 값은 외부로 노출되지 않아 확인할 수 없다.
+ Symbol 함수에 들어가는 문자열 인자는 심볼 값에 대한 description으로서 선택적으로 넣을 수 있다. 이 문자열은 디버깅 용도로만 사용되며 심볼 값 생성에 영향을 주지는 않는다.

```javascript
const a = Symbol('a')
a.description // "a"
a.toString() // "Symbol(a)"
!a // false
a + 'hi' // Uncaught TypeError
```

+ 심볼 값도 객체처럼 메서드를 사용하면 암묵적으로 *래퍼 객체를 생성한다. description 프로퍼티와 toString은 Symbol.prototype의 프로퍼티다. 심볼 값은 문자열이나 숫자 타입으로 변환되지 않는다. 단 불리언 타입으로는 타입 변환이 된다.
+ *래퍼 객체: 일시적으로 임시 객체를 만들어서 메서드나 프로퍼티를 사용할 수 있게 한 후, 역할이 끝나면 다시 원시값으로 돌아온다. 사용이 끝난 래퍼 객체는 가비지 컬렉션의 대상이 된다.
+ 객체의 프로퍼티를 symbol로 만들면 Object.`getOwnPropertyNames()` 반환 값에서 제외됩니다.
+ value에 접근할 때는 `[]`를 통해 접근해야 한다. `.`을 통해 접근하면 undefined가 반환됩니다.