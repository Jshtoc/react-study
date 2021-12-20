# React Router Hook

- 구성
  - useHistory => 많이쓰임
  - useLocation
  - useParams => 많이 쓰임
  - useRouteMatch

---

## useHistory

```javascript
// 상위에서 props를 안받고 HOC를 이용하여 받아오는 방법(1번째 방법)
import { withRouter, useHistory } from "react-router-dom";

// export default withRouter(function LoginButton(props){
//   console.log(props);
//   function login(){
//     setTimeout(()=>{
//       props.history.push('/');
//     },1000);
//   }
//   return (
//     <button onClick={login}>로그인 하기</button>
//   )
// })

// props를 받지 않고 사용하는 방법
export default function LoginButton() {
  const history = useHistory();

  function login() {
    setTimeout(() => {
      history.push("/");
    }, 1000);
  }
  return <button onClick={login}>로그인 하기</button>;
}
```

---

## useParams

```javascript
import { useParams } from "react-router-dom";

// export default function Profile(props) {
//   const id = props.match.params.id;
//   console.log(id, typeof id);
//   return (
//     <div>
//       <h2>Profile page</h2>
//       {id && <p>id는 {id} 입니다.</p>}
//     </div>
//   );
// }

export default function Profile() {
  const params = useParams();
  const id = params.id;
  console.log(id, typeof id);
  return (
    <div>
      <h2>Profile page</h2>
      {id && <p>id는 {id} 입니다.</p>}
    </div>
  );
}
```

코드의 간결화가 되는 편한 훅이므로 알아두자
