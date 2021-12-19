# Custom Hook(useSomthing)

반복적으로 사용해야 할 경우 따로 만들어 사용에 편리하도록 만든 훅

ex)

```javascript
import { useEffect, useState } from "react";

export default function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const resize = () => {
      setWidth(window.innerWidth);
    };
    window.addEventListener("resize", resize);

    return () => {
      window.removeEventListener("resize", resize);
    };
  }, []);

  return width;
}
```

윈도우 가로 넓이가 변경될 때 마다 실행되는 훅

---

<br>
<br>

# useHasMounted vs withHasMounted

## withHasMounted

**HOC 인자로 넣어진 component에 hasMounted라는 props 포함한다.**

```javascript
import React from "react";

export default function withHasMounted(Component) {
  class NewComponent extends React.Component {
    state = {
      hasMounted: false,
    };
    render() {
      const { hasMounted } = this.state;
      return <Component {...this.props} hasMounted={hasMounted} />;
      // unrelated props 는 그냥 통과시켜줘야 하므로 NewComponent에 있는 this.props를 통과시켜줘야한다.
    }
    componentDidMount() {
      this.setState({ hasMounted: true });
    }
  }

  NewComponent.displayName = `withHasMounted(${Component.name})`;
  // displayName 을 하는 이유는 디버깅할때 좋음 설정안할경우 undefined

  return NewComponent;
}
```

---

## useHasMounted

_Mounted 됐을 때 알려줌_

```javascript
import { useEffect, useState } from "react";
// useState로 만들고 useEffect로 변경하는 형태

export default function useHasMounted() {
  const [hasMounted, setHasMounted] = useState(false);

  useEffect(() => {
    setHasMounted(true);
  }, []);

  return hasMounted;
}
```

코드가 간결한 이유인지는 모르겟으나 HOC보다 hook을 사용하는 트렌드
