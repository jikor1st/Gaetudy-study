primitive(원시) type 과 reference(참조) type
======

<br>

### Primitive Type (원시타입)

> Primitive Type 은 값(Value) 자체를 변수에 직접 저장합니다. 변수가 실제 값을 직접 가지고 있다는 것을 의미합니다.

다음은 자바스크립트에서 사용되는 Primitive Type 들입니다.

- `boolean` : 불리언 값 (true or false)을 저장합니다.
- `number` : 숫자 값을 저장합니다. 정수, 소수, 음수 등 모든 숫자 값을 저장합니다.
- `string` : 문자열 값을 저장합니다. 따옴표(') 또는 쌍따옴표(")로 둘러싸인 문자열을 저장합니다.
- `null` : 값이 없음을 나타냅니다
- `undefined` : 값이 지정되지 않았음을 의미합니다.

Primitive Type은 변수가 값 자체를 직접 저장하기 때문에 변수 간의 값을 비교할 때 값이 같은지를 확인할 수 있습니다.

```javascript
let a = 1;
let b = 1;

console.log(a === b); // true
```

ES6부터는 <b>`Symbol`</b> 이라는 새로운 Primitive Type 이 추가되었습니다. Symbol 은 유일한 값을 나타내는데 사용됩니다. Symbol 은 객체의 프로퍼티나 맵의 키로 사용되며, 유일성이 보장되기 때문에 다른 값과 충돌하지 않습니다.

다음은 Symbol을 사용한 예시입니다.

```javascript
let symbol1 = Symbol();
let symbol2 = Symbol();

console.log(symbol1 === symbol2); // false

let obj = {
  [symbol1]: 'value1',
  [symbol2]: 'value2'
};

console.log(obj[symbol1]); // 'value1'
console.log(obj[symbol2]); // 'value2'
```

위의 코드에서 `symbol1`과  `symbol2`는 각각 새로운 유일한 Symbol 값을 가지고 있습니다. 따라서 `symbol1 === symbol2`의 결과는 `false`가 반환됩니다.

또한 `obj` 객체의 프로퍼티로 Symbol 값을 사용하면, 해당 프로퍼티는 일반적인 문자열 프로퍼티와 구분됩니다. 위의 코드에서는 `[symbol1]`과 `[symbol2]`로 Symbol 값을 사용하여 객체의 프로퍼티를 추가하고, `obj[symbol1]`과 `obj[symbol2]`로 프로퍼티 값을 조회할 수 있습니다. 

### Reference Type (참조 타입)
> Reference Type은 값이 있는 위치(주소)를 변수에 저장합니다. 변수가 같이 있는 메모리 주소를 가리키고 있다는 것을 의미합니다.

다음은 자바스크립트에서 사용되는 Reference Type 들입니다.

- `object` : 객체를 저장합니다. 객체는 여러 개의 프로퍼티와 메서드를 가질 수 있습니다. 
- `array` : 배열을 저장합니다. 배열은 여러 개의 요소를 가질 수 있습니다. 
- `function` : 함수를 저장합니다. 함수는 실행 가능한 코드 블록입니다.

Reference Type은 변수가 값이 있는 메모리 주소를 가리키고 있기 떄문에, 변수간의 값을 비교할 때 값이 같은지를 확인할 수 없습니다. 

```javascript
let obj1 = { a: 1 };
let obj2 = { a: 1 };

console.log(obj1 === obj2); // false
```

위의 코드에서 `obj1`과 `obj2`는 `{ a: 1 }`라는 같은 값을 가지고 있지만, 서로 다른 주소를 가리키고 있기 때문에 `===` 비교 연산자로 값을 비교하면 `false`가 반환됩니다. 

ES6 부터는 <b>`Map`, `Set`, `WeakMap`, `WeakSet`, `Date`, `RegExp`, `Error`</b> 등의 새로운 Reference Type도 추가되었습니다.