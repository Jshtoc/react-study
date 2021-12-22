# React Testing

**방법**

1. JavaScript Unit Test
2. Jest 사용하기
3. React Component Test
4. testing-library/react 활용하기
5. enzyme 활용하기

---

## JavaScript Unit Test

- facebook/jest

```
1. mkdir jest-example 폴더생성
2. cd jest-example 폴더 접속
3. npm init -y npm 설치
4. npm i jest -D
5. code . 실행
```

package.json 폴더안

```javascript
{
  "name": "jest-example",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "jest"
    // test : "@@@@@" 부분을 jest 로 수정
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "jest": "^27.4.5"
  }
}

```

자동실행 명령어

```
npx jest --watchAll
```

example.test.js 파일 생성

```javascript
describe("expect test", () => {
  it("37 to equal 37", () => {
    expect(37).toBe(37);
  });
  it("{age:39} to equal {age:39}", () => {
    expect({ age: 39 }).toEqual({ age: 39 });
  });
  it(".toHaveLength", () => {
    expect("hello").toHaveLength(5);
    // 길이 구해서 비교해볼때 사용.
  });
  it(".toHaveProperty", () => {
    expect({ name: "Jung" }).toHaveProperty("name");
    expect({ name: "Jung" }).toHaveProperty("name", "Jung");
  });
  it(".toBeDefined", () => {
    expect({ name: "Jung" }.name).toBeDefined();
    // undefined 랑 동일
  });
  it(".toBeFalsy", () => {
    expect(false).toBeFalsy();
    expect(0).toBeFalsy();
    expect("").toBeFalsy();
    expect(null).toBeFalsy();
    expect(undefined).toBeFalsy();
    expect(NaN).toBeFalsy();
  });
  it(".toBeGreaterThan", () => {
    expect(10).toBeGreaterThan(9);
    // 10 이 9보다 커야함
  });
  it(".toBeGreaterThanOrEqual", () => {
    expect(10).toBeGreaterThanOrEqual(10);
    // 10 이 뒤의 값보다 크거나 같아야함
  });
  it(".toBeInstanceOf", () => {
    class Foo {}
    expect(new Foo()).toBeInstanceOf(Foo);
    // 에러의 자식인 에러를 쓰로우한다음 어디 에러인지 구분용도
  });
});
```

![to](https://user-images.githubusercontent.com/93709088/147104024-5faddb85-66cf-4f4a-a88f-e43d8c7740ac.PNG)

---

![notTo](https://user-images.githubusercontent.com/93709088/147104097-322db6ad-d07d-408b-b2ca-1ed7a860a268.PNG)

---

![async](https://user-images.githubusercontent.com/93709088/147104131-361c50b7-e91a-48da-a507-52b6bfa486a6.PNG)

비동기로직 테스트에 가장 많이 쓰이는 방식.

## React Component Test

준비과정

```
1. npx create-react-app@5.0.0 react-component-test // 폴더생성
```
