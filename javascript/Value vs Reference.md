### Value vs Reference

+ 자바스크립트는 값에 의한 전달(passed by value) 이 일어나는 6가지의 데이터타입(Boolean, Null, Undefined, String, Number, Symbol)을 가지고 있습니다. 우리는 이러한 데이터 타입을 원시 타입(Primitive Types) 이라고 부릅니다.
+ 또 자바스크립트는 참조에 의한 전달(passed by reference) 이 일어나는 3가지의 데이터 타입(Array, Function, Object)도 가지고 있습니다. 사실 이 3가지는 크게 보자면 전부 객체(Objects)로 볼 수 있습니다.

#### Value

+  원시타입은 immutable data type 이기 때문에 ,값이 변경될 경우, 새로운 값을 할당을 받습니다.

```javascript
let a = 50;
let b = a;

a = 10;

console.log(b); // 50
```

![value](https://user-images.githubusercontent.com/67888402/144185202-724823dd-24db-4f6b-9e99-40f608b222b9.png)

+ 위의 상황에서 a나 b의 값을 수정 하더라도 a와 b의 값이 전부 바뀌지 않는다. 왜냐하면 주소가 같은 것이 아니라 값을 Copy & Paste 했기 때문이다.



#### Reference

```javascript
let a = ["kimchi", "soju"];
let b = a;
console.log(b); // ["kimchi", "soju"]

a.push("doenjang");
console.log(b); // ["kimchi", "soju", "doenjang"]

b.push("makgeolli");
console.log(a); // ["kimchi", "soju", "doenjang", "makgeolli"]
```

![reference](https://user-images.githubusercontent.com/67888402/144186370-182f53a9-8bc5-4095-a7af-41131d38c3e4.png)

+ Reference는 Value 와는 다르게 Reference를 Copy & Paste한다.