# Context API

**context를 이용하면 단계마다 일일이 props를 넘겨주지 않고도 컴포넌트 트리 전체에 데이터를 제공할 수 있습니다.**

일반적인 React 애플리케이션에서 데이터는 위에서 아래로 (즉, 부모로부터 자식에게) props를 통해 전달되지만,  
애플리케이션 안의 여러 컴포넌트들에 전해줘야 하는 props의 경우  
(예를 들면 선호 로케일, UI 테마) 이 과정이 번거로울 수 있습니다.  
context를 이용하면, 트리 단계마다 명시적으로 props를 넘겨주지 않아도 많은 컴포넌트가 이러한 값을 공유하도록 할 수 있습니다.

## 하위 컴포넌트 전체에 데이터를 공유하는 법

- 데이터를 Set 하는 놈
  - 가장 상위 컴포넌트 => 프로바이더
- 데이터를 Get 하는 놈
  - 모든 하위 컴포넌트에서 접근 가능
    - 컨슈머로 하는 방법
    - 클래스 컴포넌트의 this.context 로 하는 방법
    - 펑셔널 컴포넌트의 useContext 로 하는 방법

## 데이터를 Set 하기

1. 일단 컨텍스트를 생성한다.
2. 컨텍스트.프로바이더를 사용한다.
3. value 를 사용

src/contexts 폴더 생성 후 안에 PersonContext.js 생성

```javascript
import React from "react";

const PersonContext = React.createContext();

export default PersonContext;
```

src/index.js 수정

```javascript
import PersonContext from "./contexts/PersonContext";

const persons = [
  { id: 0, name: "seung-ho", age: 26 },
  { id: 1, name: "Seck", age: 22 },
];
// 전역에서 사용가능

ReactDOM.render(
  <React.StrictMode>
    <PersonContext.Provider value={persons}>
      <App />
    </PersonContext.Provider>
  </React.StrictMode>,
  document.getElementById("root")
);
```

---

## 데이터를 Get 하기(1) - Consumer

1. 컨텍스트를 가져온다.
2. 컨텍스트.컨슈머를 사용한다.
3. value 를 사용.

src/components 폴더안 컴포넌트 생성

```javascript
import PersonContext from "../contexts/PersonContext";

export default function Example1() {
  return (
    <PersonContext.Consumer>
      {/* PersonContext안에 있는 value랑 같은값이므로 persons라 해도 동일. */}
      {(persons) => (
        <ul>
          {persons.map((person) => (
            <li>{person.name}</li>
          ))}
        </ul>
      )}
    </PersonContext.Consumer>
  );
}
// function 컴포넌트와 class 컴포넌트에서 범용적으로 사용된다.
```

---

## 데이터를 Get 하기 (2) - class

1. static contextType에 컨텍스트를 설정한다.
2. this.context => value 이다.

```javascript
import React from "react";
import PersonContext from "../contexts/PersonContext";

export default class Example2 extends React.Component {
  // static contextType = PersonContext;
  // 여러개를 사용할 수 없다는게 단점.

  render() {
    const persons = this.context;
    return (
      <ul>
        {persons.map((person) => (
          <li>{person.name}</li>
        ))}
      </ul>
    );
  }
}

Example2.contextType = PersonContext;
```

---

## 데이터를 Get 하기 (3) - functional

1. useContext 로 컨텍스트를 인자로 호출한다.
2. useContext 의 리턴이 value이다.

```javascript
import { useContext } from "react";
import PersonContext from "../contexts/PersonContext";

export default function Example3() {
  const persons = useContext(PersonContext);
  //  훅을 사용
  return (
    <ul>
      {persons.map((person) => (
        <li>{person.name}</li>
      ))}
    </ul>
  );
}

// 많이 쓰이는 방식
```
