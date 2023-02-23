# this

## 개요

this는 자기 자신을 참조할 수 있는 객체를 말합니다.

다음과 같이 rect의 `width`와 `height`를 곱하여 사각형의 면적을 구하는 `getSquareMeter` 메서드가 있습니다.
`getSquareMeter` 메서드는 자기자신인 rect과 width와 height 프로퍼티를 재귀적으로 참조할 수 있습니다.
객체 리터럴은 변수 선언문에 할당하기 직전에 평가되어 이미 객체가 생성되어서 자기 자신을 참조할 수 있는 것입니다.
하지만 이와 같이 자기 자신이 속한 객체를 재귀적으로 참조하는 방식은 권장되지 않습니다.

```javascript
const rect = {
  width: 5,
  height: 5,
  getSquareMeter() {
    return rect.width * rect.height;
  },
};

const squareMeter = rect.getSquareMeter();
console.log(squareMeter); // 25;
```

javascript는 이때 사용할 수 있는 this라는 식별자를 제공해줍니다.

this를 사용하면 위와 같은 로직을 아래와 같이 바꿀 수 있습니다.

```javascript
const rect = {
  width: 5,
  height: 5,
  getSquareMeter() {
    return this.width * this.height;
  },
};

const squareMeter = rect.getSquareMeter();
console.log(squareMeter); // 25;
```

## this란

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-reference variable)입니다.
여기서 말하는 자신이 속한 객체와 생성할 인스턴스란 다음과 같은 상황을 말합니다.

```javascript
const rect = {
  // 자신이 속한 객체
  width: 10,
  height: 10,
  getSquareMeter() {
    return this.width * this.height;
  },
};

class Rect {
  // 생성할 인스턴스
  constructor() {
    this.width = 10;
    this.height = 10;
  }

  getSquareMeter() {
    return this.width * this.height;
  }
}
```

## 바인딩

바인딩이란 식별자와 값을 연결하는 과정을 말합니다.
예를들어 변수 선언은 변수 이름과 확보된 메모리 공간의 주소를 바인딩 하는 것입니다.

### 그럼 `this 바인딩` 이란 무엇일까요?

this 바인딩은 this가 가리킬 객체를 정하는 과정을 말합니다.
this가 결정되는 시점은 호출 방식에의해 결정이 됩니다.

## 주관적인 견해

우선 this에 대한 주관적인 생각을 말하면 함수에서 this를 호출하는 것은 좋지 않은 방법이라고 생각이 듭니다.
위에서 말했듯이 호출 방식에의해 this가 결정된다면, 사용자(개발자)가 사용하는 방식에 따라서 this의 동작 방식이 달라질 수 있다는 것인데, 그러면 예상치 못한 결과와 오류를 발생시킬 수 있을것 입니다.

우선 함수를 일반 함수로 호출했을 때와 new 생성자를 통해서 호출했을때를 비교해보겠습니다.

1. 일반 함수로 후출했을 때와 new 생성자로 호출하는 함수의 this 바인딩
   ( 아래의 예제는 index.html에서 자세히 설명이 됩니다. )

   일반적으로 함수 내부에서 this를 호출하면 전역객체인 window를 가리킵니다.
   하지만 함수를 new 생성자를 통해서 호출하면 해당 함수 객체를 가리킵니다(함수도 하나의 객체입니다)

   ```javascript
   function person() {
     this.name = "Jone";
     this.age = 18;
     console.log(this);
   }

   person(); // window 객체에 name과 age 프로퍼티가 생성이 된다. (의도한 바가 아님.)

   function Person() {
     this.name = "Jone";
     this.age = 18;
     console.log(this);
   }

   new Person(); // Person {name:'Jone', age:18}
   ```

일반 함수를 호출하게 되면 의도치 않은 동작을 수행하고, 그로 인해서 버그가 발생할 수도 있습니다.
예를들어서 window에 기본적으로 등록되어 있는 log property를 의도치 않고 this로 덮어씌우면 해당 프로퍼티를 원하는 동작대로 사용할 수 없을 것입니다.
위와 같이 전역 객체를 망가뜨리고 버그 투성이로 만들 여지를 남겨두는 행위를 막을 수 있는 방법이 있습니다.

## "use strict"

`use strict` 모드를 사용하면 자바스크립트 언어의 문법을 엄격하게 적용시켜 오류가 발생할 가능성이 높거나 자바스크립트의 최적화 작업에 문제를 일으킬 수 있는 코드에 명시적인 에러를 발생시킵니다.

use strict를 사용하여 얻는 이점은 많지만 이번 글에서는 this와 연관되어 있는 것만 다뤄보려 합니다.

use strict를 사용하면 일반적인 함수 호출에서는 this는 undefined가 반환됩니다.
더이상 this로 window에 접근을 할 일이 없어졌습니다.

```javascript
"use strict";
function Person() {
  console.log(this); // undefined
}
Person();
```
