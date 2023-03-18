# Primitive Value

```javascript
const number = new Number();

console.log(number);
/*
[[Prototype]]: Number
[[PrimitiveValue]]: 0
*/
```

위의 코드를 실행하면 `PrimitiveValue` 라는 것이 객체안에 담겨져 있습니다. 이것은 `Boolean`, `String` 일때도 동일하게 나옵니다.

Primitive Value는 원시값, 단순값이라고 하고 더이상 단순화 할 수 없는 값이라고 할 수 있습니다.

## Primitive Type의 종류

Primitive Value이 원시 값이였다면 Primitive Type은 원시 타입으로 설명 할 수 있습니다.
또 다르게는 객체가 아닌 값을 가질 수 있는 자료형입니다.

! 자바스크립트에서는 객체, 함수, 배열 모두 객체입니다.

- string
- number
- bigint
- boolean
- symbol
- undefined
- null

## Primitive Type 변수 할당

원시 타입의 값은 변수에 할당 될 때 메모리 상에 고정된 크기로 저장이 되고 해당 변수가 원시 데이터 값을 보관합니다.
변수 선언, 초기화, 할당시 값이 저장된 메모리 영역에 직접적으로 접근하여 할당된 메모리 블럭에 저장된 값을 바로 변경합니다.
한마디로 하나의 메모리 공간에 할당된 값만 들어갑니다.

## Primitive Type 변수 복사

원시 타입의 값을 각 변수간에 복사를 할 경우에, 값이 복사됩니다.
복사된 기존의 값을 다른 값으로 변경한다고 해서 복사된 변수의 값이 바뀌지 않습니다. 이 점은 reference type과 크게 다른점입니다.

```javascript
let a = 10;
let b = a;

a = 8;

console.log(b);
// 10
```

<!--  -->

https://velog.io/@bining/javascript-%EC%9B%90%EC%8B%9C%ED%83%80%EC%9E%85primitive-type-VS-%EC%B0%B8%EC%A1%B0%ED%83%80%EC%9E%85reference-typefeat.-stack%EA%B3%BC-heap-%EC%98%81%EC%97%AD
