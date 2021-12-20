# 컴포넌트 간 통신

## 하위 컴포넌트 변경하기

- A의 button 을 클릭하여 E 를 변경하려면

  1. `<A />` 컴포넌트에서 button 에 onClick 이벤트를 만들고,
  2. button을 클릭하면, `<A />`의 state를 변경하여, `<B />`로 내려주는 props를 변경
  3. `<B />`의 props 가 변경되면, `<C />` 의 props 에 전달
  4. `<C />`의 props 가 변경되면, `<D />` 의 props 에 전달
  5. `<D />`의 props 가 변경되면, `<E />` 의 props 에 전달

```javascript
// A 컴포넌트
<div>
  <B />
  <button>클릭</button>
</div>
================================

// B 컴포넌트
<div>
  <C />
</div>
================================

// C 컴포넌트
<div>
  <D />
</div>
================================

// D 컴포넌트
<div>
  <E />
</div>
================================

// E 컴포넌트
<div>
  {props.value}
</div>
================================
```

```javascript
import { useState } from "react";

export default function A() {
  const [value, setValue] = useState("아직 안바뀜");
  return (
    <div>
      <B value={value} />
      <button onClick={click}>E 의 값을 바꾸기</button>
    </div>
  );

  function click() {
    setValue("E의 값을 변경");
  }
}

function B({ value }) {
  return (
    <div>
      <p>여긴 B</p>
      <C value={value} />
    </div>
  );
}

function C({ value }) {
  return (
    <div>
      <p>여긴 C</p>
      <D value={value} />
    </div>
  );
}

function D({ value }) {
  return (
    <div>
      <p>여긴 D</p>
      <E value={value} />
    </div>
  );
}

function E({ value }) {
  return (
    <div>
      <p>여긴 E</p>
      <h3>{value}</h3>
    </div>
  );
}
```

---

## 상위 컴포넌트 변경하기

- E의 button 을 클릭하여 A 의 p를 변경하려면

  1. `<A />`에 함수를 만들고, 그 함수 안에 state를 변경하도록 구현, 그 변경으로 인해 p 안의 내용을 변경.
  2. 만들어진 함수를 props 에 넣어서, `<B />`로 전달
  3. `<B />`의 props 의 함수를, `<C />` 의 props 로 전달
  4. `<C />`의 props 의 함수를, `<D />` 의 props 로 전달
  5. `<D />`의 props 의 함수를, `<E />` 의 props 로 전달, `<E />`에서 클릭하면 props로 받은 함수를 실행

  <br>

```javascript
// A 컴포넌트
<div>
  <B />
  <p>{state.value}</p>
</div>
================================

// B 컴포넌트
<div>
  <C />
</div>
================================

// C 컴포넌트
<div>
  <D />
</div>
================================

// D 컴포넌트
<div>
  <E />
</div>
================================

// E 컴포넌트
<div>
  <button>클릭</button>
</div>
================================

```

<br>

```javascript
// 상위 컴포넌트 변경하기

import { useState } from "react";

export default function A() {
  const [value, setValue] = useState("아직 안바뀜");
  return (
    <div>
      <p>{value}</p>
      <B setValue={setValue} />
    </div>
  );
}

function B({ setValue }) {
  return (
    <div>
      <p>여긴 B</p>
      <C setValue={setValue} />
    </div>
  );
}

function C({ setValue }) {
  return (
    <div>
      <p>여긴 C</p>
      <D setValue={setValue} />
    </div>
  );
}

function D({ setValue }) {
  return (
    <div>
      <p>여긴 D</p>
      <E setValue={setValue} />
    </div>
  );
}

function E({ setValue }) {
  return (
    <div>
      <p>여긴 E</p>
      <button onClick={click}>클릭</button>
    </div>
  );

  function click() {
    setValue("A 의 값을 변경");
  }
}
```
