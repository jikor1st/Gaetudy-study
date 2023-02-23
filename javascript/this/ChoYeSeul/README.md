# This

> this란 함수를 호출할 때 생성되는 **실행 컨텍스트 객체**이다.
>
> > 실행 컨텍스트란, 실행할 코드에 제공할 환경 정보들을 모아놓은 객체

- 자바스크립트에서 this의 값(== this 바인딩)은 함수를 호출한 방법에 따라 바뀐다.
- 함수를 호출하면 인자(argument)와 this가 암묵적으로 함수 내부에 전달된다.
  <br />

### 전역 실행 맥락에서 this

전역 실행 맥락에서 `this`는 전역 객체를 참조한다.

```js
console.dir(this); // window 객체가 나온다.
console.dir(window); // window 객체가 나온다.
console.log(this === window); // true
```

`var`로 변수를 선언하고 할당하면 전역 객체 안의 프로퍼티로 해당 변수를 할당한다. const와 let은 안됨.

```js
var name = "mint";
console.log(this.name); // "mint"
console.log(window.name); // "mint"

const age = "8";
console.log(this.age); // undefined
console.log(window.age); // undefined

let favorite = "tomato";
console.log(this.favorite); // undefined
console.log(window.favorite); // undefined
```

<br />
### 함수에서의 this

기본적으로 `this`는 전역 객체에 바인딩된다. 전역 함수, 내부 함수 가리지 않는다.

```js
function second() {
  console.log(this);

  function first() {
    console.log(this);
  }

  first(); // window 객체
}
second(); // window 객체
```

또한 함수의 호출하는 방식은 아래와 같다.
<br />

#### (1) 메소드 내의 this

메소드의 내부 함수(== 객체안에 선언된 함수)일 경우엔 `this`는 현재 함수를 실행하고 있는 그 객체를 참조한다(바인딩된다).

```js
var obj = {
  methodA: function () {
    console.log("obj -> methodA's this : " + this); // obj
  },
  inner: {
    methodB: function () {
      console.log("obj -> inner -> methodB's this : " + this); // obj.inner
    },
  },
};
```

고차 함수의 콜백 함수 안에서 this는 콜백 함수가 일반 함수이기 때문에 전역 객체를 참조한다.

```js
const obj = {
  name: "Kim",
  arr: [1, 2, 3],
  showArr() {
    this.arr.forEach((el) => {
      console.log(el);
      console.log(this); // window
    });
  },
};
obj.showArr(); // this에 window객체 출력된다.
```

위의 상황의 해결 방법으로 콜백함수 다음 인자로 참조할 객체를 전달해 줄 수 있다.

```js
const obj = {
  name: "Kim",
  arr: [1, 2, 3],
  showArr() {
    this.arr.forEach((el) => {
      console.log(el);
      console.log(this);
    }, this);
  },
};
obj.showArr(); // this에 obj객체가 출력된다.
```

<br />

#### (2) 이어서 진행 예정

참고

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this
- https://eunjinii.tistory.com/104
- https://hanamon.kr/javascript-this%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/
- https://velog.io/@realryankim/JavaScript-this%EB%9E%80
- https://poiemaweb.com/js-this
