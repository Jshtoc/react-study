# Additional Hooks

- 구성
  - useReducer
  - useCallback,useMemo
  - useRef, ~~useImperativeHandle~~
  - ~~useLayoutEffect~~
  - ~~useDebugValue~~

---

## useReducer

- 특징
  - 다수의 하윗값을 포함하는 복잡한 정적 로직을 만드는 경우
  - 다음 state가 이전 state에 의존적인 경우
  - Redux 를 안다면 쉽게 사용 가능

```javascript
import { useReducer } from "react";

// reducer => state 를 변경하는 로직이 담겨 있는 함수
const reducer = (state, action) => {
  if (action.type === "PLUS") {
    return {
      count: state.count + 1,
    };
  }
  return state;
};

// dispatch => action 객체를 넣어서 실행

// action => 객체이고 필수 프로퍼티로 type 을 가진다.

export default function Example6() {
  const [state, dispatch] = useReducer(reducer, { count: 0 }); // useReducer(reducer는 함수 , 초기값)

  return (
    <div>
      <p>You Clicked {state.count} times</p>
      <button onClick={click}>Click me</button>
    </div>
  );

  function click() {
    dispatch({ type: "PLUS" });
  }
}

// useReducer 는 다수의 하위값을 포함하는 복잡한 state일경우 사용하면 좋다
// 이전 state를 가지고있다가 action과 조합해서 새로운 state를 만드는경우에 이전 state에 의존하는거기 때문에 좋다.
```

---

## useCallback, useMemo

```javascript
import { useCallback, useMemo, useState } from "react";

function sum(persons) {
  console.log("sum...");

  return persons.map((person) => person.age).reduce((l, r) => l + r, 0);
}
export default function Example7() {
  const [value, setValue] = useState("");
  const [persons] = useState([
    { name: "Mark", age: 39 },
    { name: "Seung-ho", age: 26 },
  ]);

  const count = useMemo(() => {
    return sum(persons);
  }, [persons]); // 저장소 개념

  const click = useCallback(() => {
    console.log("useCallback", value);
  }, []); // useEffect componetDidMount의 최초에만 이함수가 생성되게 하는 방식
  // dependency array에 의존해서 필요시에만 부르는 함수 = useCallback

  return (
    <div>
      <input value={value} onChange={change} />
      <p>{count}</p>
      <button onClick={click}>click</button>
    </div>
  );

  function change(e) {
    setValue(e.target.value);
  }
}
```

---

## useRef

```javascript
import { createRef, useRef, useState } from "react";

export default function Example8() {
  const [value, setValue] = useState("");
  const input1Ref = createRef(); // 항상 래퍼런스를 생성해서 렌더될때마다 넣어줌.
  const input2Ref = useRef(); // 렌더 사이에도 유지해줌.
  // 렌더 사이에 어떤 상태를 유지해주는 경우. 클래스컴포넌트에선 상관없지만 function같은 경우에는 계속 새로 생성되기때문에 상태를 유지하는 경우가 필요하다.

  console.log(input1Ref.current, input2Ref.current);

  return (
    <div>
      <input value={value} onChange={change} />
      <input ref={input1Ref}></input>
      {/* controlled ref */}
      <input ref={input2Ref}></input>
      {/* unControlled ref */}
    </div>
  );

  function change(e) {
    setValue(e.target.value);
  }
}
```
