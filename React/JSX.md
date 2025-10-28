# 개요
- JSX (JavaScript XML)는 자바스크립트 안에서 HTML 태그처럼 UI 구조를 표현할 수 있게 해주는 문법.

# 특징
## 1. 반드시 하나의 부모요소만을 리턴해야 함
``` ts
return (
  <h1>제목</h1>
  <p>본문</p>   //이런 구조 안됨
);
```

## 2. ### 조건문 / 반복문은 JSX 안에서 직접 못 씀
- 대신 삼항연산자나 map() 함수 사용
``` ts
{isLogin ? <Dashboard /> : <LoginPage />}

{users.map(user => (
  <UserCard key={user.id} name={user.name} />
))}
```

