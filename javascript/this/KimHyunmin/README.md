JavaScript 에서의 "this"
======

>JavaScript에서 "this"는 함수가 호출될 때 실행 컨텍스트 내에서 현재 객체를 나타내는 특별한 키워드입니다. "this"를 사용하여 함수 내에서 현재 객체를 참조하고, 객체의 프로퍼티 및 메서드에 액세스할 수 있습니다.

<br>

### "this"의 값은 함수를 호출하는 방법에 따라 결정됩니다.

#### 1. 함수 호출

함수를 일반적인 방법으로 호출할 때 "this"는 전역 객체를 참조합니다. 하지만 "use strict" 모드에서는 전역 객체를 참조하지 않고 "undefined"를 반환합니다.

```javascript
function foo() {
  console.log(this); // 전역 객체 (브라우저에서는 window 객체)
}

foo();
```

#### 2. 메서드 호출

객체의 메서드를 호출할 때 "this"는 해당 객체를 참조합니다.

```javascript
const obj = {
  name: "Gaetudy",
  sayName() {
    console.log(this.name); // obj 객체의 name 프로퍼티
  }
};

obj.sayName();
```

#### 3. 생성자 함수 호출
생성자 함수를 사용하여 객체를 생성할 때 "this"는 새로 생성된 객체를 참조합니다.

```javascript
function Person(name) {
  this.name = name;
}

const person1 = new Person("Kim");
console.log(person1.name); // "Kim"

```

#### 4. apply(), call() 및 bind() 메서드 호출
apply(), call(), bind() 메서드를 사용하여 함수를 호출할 때 "this"는 첫번째 인수로 전달된 객체를 참조합니다.

```javascript
function foo() {
  console.log(this.name);
}

const obj1 = { name: "Harry" };
const obj2 = { name: "Son" };

foo.call(obj1); // "Harry"
foo.apply(obj2); // "Son"

const boundFoo = foo.bind(obj1);
boundFoo(); // "Harry"
```
<br>
### 예제를 통해 "this" 설명해보기
"person" 이라는 객체를 만들고, 그 객체의 이름과 니이를 출력하는 함수인 "sayHi"를 만든 예제입니다.

```javascript
let person = {
    name: "현민",
    age: 26,
    sayHi: function() {
        console.log("안녕하세요. 제 이름은 " + this.name + "입니다." + " 그리고 저는 " + this.age + "살 입니다.");
    };
};

person.sayHi(); // 출력 결과: "안녕하세요. 제 이름은 현민입니다. 그리고 저는 26살 입니다."
```
위 예제에서 "this" 는 "person" 객체를 참조합니다. "sayHi" 함수가 속한 객체는 "person"이기 때문에, "this"는 "person"을 가리키게 됩니다. 따라서 "sayHi" 함수 내에서 "this.name"과 "this.age"를 사용하면, 해당 객체의 이름과 나이를 출력할 수 있습니다. 
##### <b>하지만 "this"는 함수를 호출하는 방식에 따라 값이 달라질 수 있으니 잘 파악해야 합니다...</b>
<br>
### 오늘의 1차 정리... 

JavaScript에서 "this"는 실행 컨텍스트 내에서 현재 객체를 나타내는 특별하고 특수한 키워드입니다. "this"의 값은 함수를 호출하는 방법에 따라 결정되며, "this"를 사용하여 함수 내에서 현재 객체를 참조하고, 객체의 프로퍼티 및 메서드에 액세스할 수 있습니다. "this"의 값을 올바르게 설정하는 것이 중요하며, 잘못된 사용은 예기치 않은 결과를 초래할 수 있기 때문에 잘 공부하고 파악해야 할것 같습니다...

strict 모드에서는 undefined 값으로 표출되는데 React 에서는 기본적으로 strict 모드가 탑재되어 있기 때문에 잘쓰이지 않습니다... (?)