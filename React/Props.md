# 개요
- props(properties)는 부모 컴포넌트가 자식 컴포넌트에게 데이터를 전달하는 수단

# 기본 개념
- React 컴포넌트는 함수처럼 동작합니다.
- 즉, 입력값이 있으면 (props) 그에 따라 출력(UI) 을 만들어내요.

``` ts
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

이 컴포넌트를 이렇게 호출하면:
``` ts
<Greeting name="승원" />
```

React는 내부적으로 아래처럼 동작해요
``` ts
Greeting({ name: "승원" });
```

즉, props는 그냥 **객체**예요.
{ name: "승원" } 이라는 객체가 Greeting 함수의 인자로 전달된 거예요.

그래서 props.name을 출력하면 승원이 나오는 거죠 ✅


# Props의 3가지 특징

| **특징**                      | **설명**                                    |
| --------------------------- | ----------------------------------------- |
| 1️⃣ **읽기 전용(Read-only)**    | 자식은 부모로부터 받은 props를 직접 수정할 수 없음           |
| 2️⃣ **단방향(one-way) 데이터 흐름** | 데이터는 **부모 → 자식** 방향으로만 흐름                 |
| 3️⃣ **객체 형태로 전달**           | 내부적으로는 항상 객체 (예: { name: "승원", age: 24 }) |

# 예시
## 1. 문자열 전달

``` ts
<Title text="OSSU 프로젝트" />

function Title(props) {
  return <h1>{props.text}</h1>;
}
```



## 2. 숫자, 불린값 전달

``` ts
<Button size={20} disabled={true} />
```



## 3. 함수 전달 (이벤트 핸들러)

``` ts
<Counter onClick={() => alert("클릭됨")} />

function Counter(props) {
  return <button onClick={props.onClick}>Click me</button>;
}
```
➡️ 부모가 자식에게 **동작(함수)** 을 전달할 수도 있습니다.
이게 React에서 상호작용을 만드는 기본 구조예요.


## 4. 객체/배열 전달

``` ts
<UserCard user={{ name: "승원", age: 26 }} />
```

``` ts
function UserCard(props) {
  return <div>{props.user.name} ({props.user.age})</div>;
}
```

# props와 state의 차이

|**구분**|**props**|**state**|
|---|---|---|
|정의|부모가 내려준 값|컴포넌트 내부에서 관리하는 값|
|수정 가능 여부|❌ 수정 불가 (읽기 전용)|✅ setState()로 변경 가능|
|소유자|부모 컴포넌트|자신 (컴포넌트 내부)|
|역할|외부 데이터 입력|내부 동작 상태 관리|

# 예제로 쉽게 비교

``` ts
function Counter({ start }) {
  const [count, setCount] = useState(start); // props로 초기값 받음
  return (
    <div>
      <p>현재 카운트: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}

// 부모
<Counter start={10} />
```
- start는 부모가 준 **props (입력값)**
- count는 내부적으로 변하는 **state (상태)**
