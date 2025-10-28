#Hook 

# 개요
- 값을 기억하는 [[useMemo]]와 달리 함수자체를 기억하는 Hook

# 기본문법
``` ts
const handleClick = useCallback(() => {
  console.log("Clicked!");
}, [dependency]);
```
- 3번줄의 dependency 배열의 요소가 바뀌지 않으면 handleClick함수를 새로 만들지 말고 이전 함수를 그대로 쓴다라는 뜻

# 쓰임새
## 1. 자식 컴포넌트의 props로 함수가 내려갈때
``` ts
function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = () => setCount((c) => c + 1);

  return <Child onClick={handleClick} />;
}

const Child = memo(({ onClick }) => {
  console.log("🧩 Child 렌더링됨");
  return <button onClick={onClick}>+</button>;
});
```
- Child는 React.memo()로 감싸서 props가 바뀌지 않으면 렌더링이 다시 안 되게 만들어짐
- 그런데 부모(Parent)가 렌더링될 때마다 handleClick이 새로 만들어지기 때문에 props가 변경되었다고 판단한 React는 child도 같이 리렌더링하게 됨