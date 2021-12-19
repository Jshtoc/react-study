# Hooks & Context

---

- _목차_
  1. Basic Hooks
  2. Custom Hooks
  3. Additional Hooks
  4. React Router Hooks
  5. 컴포넌트 간 통신
  6. Context API

---

## 1. Basic Hooks

- **useState**
- **useEffect**

## \*useState

_state를 대체 할 수 있다._

기존의 class component를 이용한 방식

```javascript
import React from "react";

export default class Example1 extends React.Component {
  state = { count: 0 }; // 객체

  render() {
    const { count } = this.state;

    return (
      <div>
        <p>You Clicked {count} times</p>
        <button onClick={this.click}>Click me</button>
      </div>
    );
  }

  click = () => {
    this.setState({ count: this.state.count + 1 });
  };
}
```

<br>

---

<br>

useState를 이용한 방식

```javascript
import React from "react";

export default function Example2() {
  const [count, setCount] = React.useState(0); // 위 객체 카운트의 초기값과 같다고 생각하면 된다.
  // const 뒤 배열의 앞 인덱스는 실제 useState의 카운트가 업데이트됬을때의 값 = count
  // 뒤 인덱스는 count를 바꾸는 함수
  return (
    <div>
      <p>You Clicked {count} times</p>
      <button onClick={click}>Click me</button>
      {/* <button onClick={() => setCount(count + 1)}>Click me</button> 로 하게되면 아래 function click은 필요없다.*/}
    </div>
  );

  function click() {
    setCount(count + 1);
  }
}
```

<br>

다른 예시

```javascript
import React from "react";

// useState => count
// useState => {count : 0};
export default function Example3() {
  const [state, setState] = React.useState({ count: 0 });
  return (
    <div>
      <p>You Clicked {state.count} times</p>
      <button onClick={click}>Click me</button>
    </div>
  );

  function click() {
    setState((state) => ({
      count: state.count + 1,
    }));
  }

  // setState만 사용하는게 아니라 setState가 어떤 것에 의존해서 사용하고 있는지 중요함.
  // 따른 훅들과 사용하게 되면 Dependency가 들어가게 되는데
  // setState안에서 인자로 받은것을 다시 새로운 state로 변경해서 리턴하게 되면 외부에 만들어 놓은 state에 의존하지 않게된다.
}
```

이처럼 useState는

Functional Component = Stateless Component
= Stateless Functional Component(SFC) 로 불렸지만

Functional Component != Stateless Component(FC) 로 불린다.
**because State hook**

왜 **useState** 가 도입이 된건가?

- 컴포넌트 사이에서 상태와 관련된 로직을 재사용하기 어렵다.
  - 컨테이너 방식 말고(props 이용해서 재사용), 상태와 관련된 로직
- 복잡한 컴포넌트들은 이해하기 어렵다.(사람이)
- Class 는 사람과 기계를 혼동시킨다.
  - 컴파일 단계에서 코드를 최적화하기 어렵게 만든다.
- this.state 는 로직에서 렌더 사이에 레퍼런스를 공유하기 때문에 문제가 발생할 수 있다.

---

## \*useEffect

_라이프 사이클 훅을 대체 할 수 있다._ (동등한 역할 X)

- componentDidMount
- componentDidUpdate
- componentWillUnmount
