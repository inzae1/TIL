

# Jest mocking II

#### **Jest.fn() 사용법** 

- jest는 가짜함수( mock function)를 생성할 수 있도록 `jest.fn()` 함수를 제공한다.

```javascript
const mockFn = jest.fn();
```

- `jest.fn()` 은 일반 자바스크립트 함수와 동일한 방식으로 인자를 넘겨 호출할 수 있다.

```javascript
mockFn();
mockFn(1);
mockFn("a");
mockFn([1, 2], { a: "b" });
```

- 위 가짜 함수의 호출결과는 `undefined` 이다. 어떤값을 리턴해야할지 아직 알려주지 않았기 때문이다.

```javascript
mockFn.mockReturnValue("I am a mock!");
console.log(mockFn()); // I am a mock!
```

- `mockReturnValue` 함수를 이용해서 가짜 함수가 어떤 값을 리턴해야할지 설정할 수 있다.
- 비슷한 방식으로 `mockResolvedValue(Promise가 resolve하는 값` 함수를 이용하면 가짜 비동기 함수를 만들 수 있다.

```javascript
mockFn.mockResolvedValue("I will be a mock!");
mockFn().then((result) => {
  console.log(result); // I will be a mock!
});
```
- 또한 `mockImplementation (구현 코드)` 함수를 이용하면 해당 함수를 통째로 재구현해버릴수도 있다.

```javascript
mockFn.mockImplementation((name) => `I am ${name}!`);
console.log(mockFn("Dale")); // I am Dale!
```
- 테스트를 작성할 떄 가짜함수가 진짜로 유용한 이유는 가짜 함수는 자신이 어떻게 호출되었는지 기억한다는 점 떄문이다.

```javascript
mockFn("a");
mockFn(["b", "c"]);

expect(mockFn).toBeCalledTimes(2);
expect(mockFn).toBeCalledWith("a");
expect(mockFn).toBeCalledWith(["b", "c"]);
```
- 위와 같이 가짜 함수 용 설계된 Jest Matcher인 `toBeCalled` 함수를 사용하면 가짜 함수가 몇번 호출되었고 인자로 무엇이 넘어왔었는지 검증할 수 있다.


#### **jset.spyOn() 사용법** 

- mocking 에는 spy 라는 개념이 있다. 어떤 객체에 속한 함수의 구현을 가짜로 대체하지 않고, 해당 함수의 호출 여부와 어떻게 호출되었는지만을 알아내야 할떄가 있는데 이럴떄 Jest 에서 제공하는 `jest.spyOn(object, methodName)` 함수를 이용하면 된다.

````javascript
const calculator = {
  add: (a, b) => a + b,
};

const spyFn = jest.spyOn(calculator, "add");

const result = calculator.add(2, 3);

expect(spyFn).toBeCalledTimes(1);
expect(spyFn).toBeCalledWith(2, 3);
expect(result).toBe(5);
````
- `jest.spyOn()` 함수를 이용해서 `calculator` 객체의 `add` 라는 함수에 스파이를 붙였다. 따라서 `add` 함수를 호출 후에 호출 횟수와 어떤 인자가 넘어갔는지 검증할 수 있다. 하지만 가짜함수로 대체한것은 아니기 때문에 결과값은 원래 구현대로 2와 3의 합인 5가 되는 것을 알 수 있다.