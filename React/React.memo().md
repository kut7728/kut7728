# 개요
- 렌더링 성능 최적화를 위한 고차 컴포넌트
- Props가 바뀌지 않으면, 컴포넌트를 리렌더링하지 않는다

# 예시
``` ts
const MyComponent = React.memo(function MyComponent(props) {
  console.log("렌더링됨");
  return <div>{props.value}</div>;
});
```
``` ts
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <button onClick={() => setCount((c) => c + 1)}>+</button>
      <MyComponent value="Hello" />
    </>
  );
}
```
- 버튼을 눌러 count가 증가하면 부모와 함께 자식도 리렌더링 되어야하지만
- props는 그대로이기에 React.memo() 덕분에 리렌더링 되지 않음
