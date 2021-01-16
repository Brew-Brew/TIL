# YOU DON'T KNOW JS (this와 객체 프로토타입, 비동기와 성능)

## 1장

`this`

- 렉시컬 스코프 안에 있는 뭔가를 this 레퍼런스로 참조하기란 애당초 가능하지 않다.
- 어떤 함수를 호출하면 활성화 레코드, 즉 싱행 컨텍스트가 만들어진다. 여기엔 함수가 호출된 근원 (Call stack)과 호출방법, 전달된 인자등의 정보가 담겨있다. this 레퍼런스는 그중 하나로, 함수가 실행되는 동안 이용할 수 있다.

## 2장

`this 바인딩방법`

- 기본 바인딩 (1)
- 암시적 바인딩 (2)
- 명시적 바인딩 (3)
  - call, apply
- new 바인딩 (4)

우선순위 : (4)>(3)>(2)>(1)

**es6 화살표 함수는 표준 바인딩 규칙을 무시하고 렉시컬 스코프로 this를 바인딩한다**

`new 연산자`

- 전통적인 클래스 지향언어의 생성자는 클래스에 붙은 특별한 메서드로, 인스턴스 생성시 new연산자로 호출된다.
- 자바스크립트에선 new는 의미상 클래스지향적인 기능과 아무 상관이 없다.
- 자바스크립트 생성자는 앞에 new연산자가 있을때 호출되는 일반 함수에 불과하다.
- 함수앞에 new가 붙을때 아래와 같은 일들이 일어난다.
  - 새 객체가 만들어진다.
  - 새로 생성된 객체의 [[Prototype]] 이 연결된다.
  - 새로 생성된 객체는 해당함수 호출시 this로 바인딩 된다.
  - 이 함수가 자신의 또 다른 객체를 반환하지 않는 한 new와 함께 호출된 함수는 자동으로 생성된 객체를 반환한다.

### 3장

`내장객체(생성자 형식)`

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects
- 자바스크립트 엔진은 상황에 맞게 문자열 원시 값을 내장객체(new String, new Number)로 자동 강제 변환하므로 명시적으로 객체를 생성할 일은 없다.
- 따라서, 생성자 형식은 지양하고 리터럴 형식을 사용하라고 적극권장 (new String('ddd') 와 같이 많이 사용안함)

`Object 불변성`

- Object.seal() (프로퍼티들의 configurable false로 만듬, 하지만 기존 프로퍼티들 값 수정가능 )
- Object.freeze()
  - (위의 seal 보다 강력한조치, 가장높은 불변성 처리, 기존 프로퍼티 값 수정도 불가, 하지만 레퍼런스로 참조하고있는 프로퍼티 갑있다면 영향 x)
  - (재귀로 순회하며 하위 객체도 freeze, 따라서 유의해야함)

`객체 property 존재 확인`

- in 연산자 (prototype 연쇄로 돌며 찾음)
- hasOwnProperty 확인 (프로퍼티가 객체에 있는지만 판단, prototype 연쇄로 찾지는 않음)

`for of`

- 배열에서 index 순회가 아닌 값 자체로의 순회가 가능해짐
- ES6부터
- @@iterator라는 내부 함수가 있어야함 (value[Symbol.iterator]())
- 일반 객체는 불가

### 5장

`Object.create 와 new ~~()`

- 둘 다 새 객체를 만들고, 프로토타입을 상속한다는 점에서는 동일하다.
- create로 객체를 만들었을때는 생성자를 호출하지않는다.

`[[Prototype]]`

- 자바스크립트 객체는 `[[Prototype]]`이라는 내부 프로퍼티가 있고 다른 객체를 참조하는 단순 레퍼런스로 사용
- a = new Foo()를 실행하면 생긴 객체 a(1)의 `[[Prototype]]` 이 Foo.prototype 객체 (2)와 링크로 연결이 맺어진다.
- 어떤 클래스로부터 작동을 복사하여 다른 객체에 넣는것이 아니라 링크로 두 객체를 연결한다.
- https://poiemaweb.com/js-prototype#2-prototype-vs-prototype-%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0

`prototype vs [[Prototype]]`

- https://poiemaweb.com/js-prototype#2-prototype-vs-prototype-%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0 참고
- 함수 객체는 일반 객체와는 달리 prototype 프로퍼티도 소유하게 된다.
- 주의해야 할 것은 prototype 프로퍼티는 프로토타입 객체를 가리키는 [[Prototype]] 인터널 슬롯은 다르다는 것이다. prototype 프로퍼티와 [[Prototype]]은 모두 프로토타입 객체를 가리키지만 관점의 차이가 있다.
