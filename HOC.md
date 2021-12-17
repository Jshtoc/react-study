# HOC - Higher - Order - Component

특징
-React의 컴포넌트 로직에서 재사용되는 고급 기술이다.
-React API의 구성원이 아니다.
-React의 구성적 특성에서 나오는 패턴

HOC = function(컴포넌트) { return 새로운 컴포넌트; }
HOC는 <컴포넌트>를 인자로 받아 <새로운 컴포넌트>를 리턴하는 함수

props = > 컴포넌트 => UI

컴포넌트 => HOC => 새로운 컴포넌트

사용하는법
-Use HOCs For Cross-Cutting Concerns
(횡단 관심사(Cross-Cutting Concerns), 페이지별로 같은 진행(비슷한 진행)을 쭉 이은 것)
대표적인 예 로깅(프로그램어딘가 a,b페이지를 갈때 로깅이 계속 발생, 로깅을 모아서 전문적으로 할수있게 기능을 분류한다음 여러페이지에서 사용)
-Don't Mutate the Original Component. Use Composition.
(HOC에 들어가는 인자를 변경하지 말라. 그럼 어케? 상속대신 오리지널 컴포넌트를 받아다가 여러 컴포넌트에 구성품처럼 놓고 통째인 컴포넌트를 리턴하는 방식)
-Pass Unrelated Props Through to the Wrapped Component
-Maximizing Composability
-Wrap the Display Name for Easy Debugging

주의할점
-Don't Use HOCs Inside the render Method
(HOC를 랜더 메서드안에 사용하지말라.)
-Static Methods Must Be Copied Over
-Refs Aren't Passed Through(feat.React.forwardRef)
