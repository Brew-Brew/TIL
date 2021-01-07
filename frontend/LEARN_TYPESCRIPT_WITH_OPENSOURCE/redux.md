[never관련](https://github.com/reduxjs/redux/blob/a64394d46a74fd3ee502016a12950c44605bd6a0/src/createStore.ts#L45)

- https://www.typescriptlang.org/docs/handbook/basic-types.html#never
- never는 모든 타입의 sub type이 될수 있다. 그역은 불가함
- 어떠한 함수가 값을 절대 return 하지않거나, exception을 throw할때

![picture](https://jbee.io/static/f19e5096c6cc5c8682607b9886b66c88/c1b63/type_diagram.png)

[@template](https://github.com/reduxjs/redux/blob/a64394d46a74fd3ee502016a12950c44605bd6a0/src/types/store.ts#L124)

- 주석에 @template? generic을 설명할때 쓰이는것으로 보임

[unknown](https://github.com/reduxjs/redux/blob/a64394d46a74fd3ee502016a12950c44605bd6a0/src/createStore.ts#L278)

- https://jbee.io/typescript/TS-9-unknown/ 참고
- unknown 타입으로 선언된 변수는 any를 제외한 다른 타입으로 선언된 변수에 할당될 수 없다.
- unknown 타입으로 선언된 변수는 프로퍼티에 접근할 수 없으며, 메소드를 호출할 수 없으며, 인스턴스를 생성할 수도 없다.
