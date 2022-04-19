

# Jest syntax

### **Jest 기초 문법**

```javascript
let temp;
describe("simple test", () => {
  beforeEach(() => {
    temp = 1;
  });
  
  afterEach(() => {
    temp = 0;
  });
  
  test('1 is 1', () => {
    expect(1).toBe(1);
  });
  
  test('[1,2,3] is [1,2,3]', () => {
    expect([1,2,3]).toEqual(1);
  });
})
```

#### **describe**
- 테스트 단위를 묶는 가장 큰 단위이다. 테스트 시 describe에 설명된 내용으로 테스트 단위를 크게 분류해준다.

#### **test, it**
- `test()`, `it()` 을 통해 기본 테스트를 한다.
- `test()` 와 `it()` 의 기능적 차이는 없지만 `it()`의 경우 다른 테스트 프레임워크에서 많이 사용되기 때문에 넣었다고 한다.

#### **expect**
- `expect()`안에 테스트할 변수나 값을 넣는다. 이후 `toBe`나 `toEqual`을 이용해 예측 값과 비교한다.

#### **toBe, toEqual**
- 결과 예측으로 가장 많이 쓰는 문법이다.
- toBe는 단순 비교, toEqual은 배열이나 객체 내부까지 깊은 비교를 해준다.

#### **beforeEach, afterEach**
```javascript
let temp;
describe("simple test", () => {
  beforeEach(() => {
    temp = 1;
  });
  
  afterEach(() => {
    temp = 0;
  });
  
  test('tmep is 1', () => {
    expect(temp).toBe(1); // true
  });
  
  test('temp is 1', () => {
    expect(temp).toBe(1); // true
  });
});
```
- `beforeEach` 는 `test()` 가 실행할 때마다 실행해주는 전처리기이다.
- `afterEach` 의 경우 `test()` 가 종료될 때마다 실행하는 후처리기이다.
- 따라서 위 예시에서 몇번의 테스트를 하더라도 temp는 1이 된다.