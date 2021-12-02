## == vs === vs TypeOf

#### ==

+ 자바스크립트에서 == 연산자를 쓰는 목적은 가벼운 동등 비교를 하기 위한 것이다. 

+ == 연산자는 암시적 형 변환을 수행한다.

  ``` javascript
  11 === "11" //타입이 다르므로 false
  11 == "11" // 암시적 형 변환으로 인한 true
  ```

+ undefinde, null, NaN

  ```javascript
  undefined == undefined // true
  null == null // true
  null == undefined // true
  NaN == undefined // false
  NaN == null // false
  NaN == NaN // false
  ```

#### ===

+ 자바스크립트에서 === 연산은 엄격한 동등성을 비교할 때 사용한다. 여기서 엄격한 동등성이란 타입과 값이 둘 다 같음을 의미한다.

+ true의 예시를 보면

  ```javascript
  3 === 3 // true
  'abcd' === 'abcd' //true
  true === true //true
  ```

+ false의 예시를 보면

  ```javascript
  33 === "33" // false => 타입이 다름
  "aaa" === "bbb" // false => 타입은 같지만 값이 다름
  false === 0 // false => 타입과 값이 전부 다름
  ```

+ === 은 타입과 값이 모두 같아야 true를 반환한다.

#### TypeOf

+ JavaScript의 특징 중 하나는 변수를 선언할 때 자료형을 다르게 사용하지 않는다는 것이다.

+ 하지만 데이터를 받아서 활용할 때는 안에 있는 데이터의 자료형이 어떤 것인지 구분되지 않아 불편하기도 하다. 이럴 때 typeof를 사용하여 자료형을 검사한다.

+ typeof 함수는 (boolean, null,  undefind, string, number, bigint, function, object) 타입중 하나를 string 형태로 return 함으로 어떤 타입인지 string 으로 구분하면 된다.

  ```javascript
  let value = 10
  if(typeof value == "number"){
      console.log("!!!");
  }
  ```

  ```javascript
  typeof 'abc'; // 'string'
  typeof 1; // 'number'
  typeof null; // 'object'
  typeof []; // 'object'
  typeof {}; // 'object'
  typeof function () {}; // 'function'
  ```