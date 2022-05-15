## 깊은 복사(deep copy)와 얕은 복사(shallow copy)

### 공통점

- 객체의 property들을 복사한다는 점에서는 동일

### 차이점

- 어느 수준까지 복사하느냐에 따라 나눠짐
- 얕은 복사: depth 1단계까지만 복사
- 깊은 복사: 모든 depth에 대해서 복사

### 얕은 복사(shallow copy)

- 한단계만 복사하기 때문에 중첩된 객체에 대해서는 서로 영향을 줌
  - 참조된 값 == 객체의 메모리 주소 값을 복사하기 때문
  - 복사의 개념이라기 보다는 property가 가지고 있는 메모리를 가지고 온 것

```js
const a = {
  a: 1,
  b: [1, 2, 3],
  c: { d: 1, e: 2 },
};

const b = Object.assign({}, a); //얕은 복사
b.b[1] = 20;

console.log(a.b); //[1, 20, 3]
console.log(b.b); //[1, 20, 3]
```

### 깊은 복사(deep copy)

- 메모리를 새로 할당하여 원본 객체를 복사하므로 별개의 객체가 됨
  - 값을 바꾸더라도 원본 객체와 복사한 객체는 서로 영향을 주지 않음
- 깊은 복사를 해야지만 immutable(불변 객체)
  - 불변 객체: 매번 새로운 객체를 생성

```js
const a = {
  a: 1,
  b: [1, 2, 3],
  c: { d: 1, e: 2 },
};

const b = Object.assign({}, a); //얕은 복사
b.b = Object.assign([], a.b); //깊은 복사
b.b[1] = 20;

console.log(a.b); //[1, 2, 3]
console.log(b.b); //[1, 20, 3]
```
