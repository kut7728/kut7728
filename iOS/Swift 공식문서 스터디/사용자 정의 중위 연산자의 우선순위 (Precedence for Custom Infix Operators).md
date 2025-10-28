  

**ChatGPT**

## ✅ 사용자 정의 중위 연산자 기본 문법

```Swift
infix operator +++ : MyPrecedenceGroup
```

- `infix operator`: 중위 연산자 정의
- `MyPrecedenceGroup`: 연산자의 우선순위를 결정할 사용자 정의 또는 기존의 **우선순위 그룹**

---

## 🎯 우선순위 그룹(Precedence Group) 만들기

```Swift
precedencegroup MyPrecedenceGroup {
    associativity: left
    higherThan: AdditionPrecedence
}
```

### 🔸 구성 요소 설명

|   |   |
|---|---|
|키워드|설명|
|`associativity`|결합 방향: `left`, `right`, `none`|
|`higherThan`|어떤 연산자보다 먼저 계산될지|
|`lowerThan`|어떤 연산자보다 나중에 계산될지|

---

### 📌 예시

```Swift
swift
복사편집
precedencegroup MultiplyThenAddPrecedence {
    associativity: left
    higherThan: AdditionPrecedence
}

infix operator *** : MultiplyThenAddPrecedence

func ***(lhs: Int, rhs: Int) -> Int {
    return lhs * rhs + 1
}

let result = 2 + 3 *** 4  // ***가 +보다 우선순위 높음
// 실제 계산 순서: 3 *** 4 → (3 * 4 + 1) = 13
// 결과: 2 + 13 = 15

```

---

## 🧠 Swift의 기본 우선순위 그룹 몇 가지

|   |   |   |
|---|---|---|
|그룹 이름|설명|예|
|`AssignmentPrecedence`|대입 연산자|`=`, `+=`, `-=`, etc|
|`TernaryPrecedence`|삼항 연산자|`a ? b : c`|
|`DefaultPrecedence`|사용자 연산자에 기본값||
|`LogicalDisjunctionPrecedence`|OR 연산자|`|
|`LogicalConjunctionPrecedence`|AND 연산자|`&&`|
|`ComparisonPrecedence`|비교|`==`, `<`, `>`|
|`NilCoalescingPrecedence`|nil 병합|`??`|
|`CastingPrecedence`|타입 캐스팅|`as`, `is`|
|`MultiplicationPrecedence`|곱셈, 나눗셈|`*`, `/`, `%`|
|`AdditionPrecedence`|덧셈, 뺄셈|`+`, `-`|
|`RangeFormationPrecedence`|범위|`...`, `..<`|
|`FunctionArrowPrecedence`|함수 타입 →|`(Int) -> String`|

---

## 🔄 결합 방향 associativity

|   |   |   |
|---|---|---|
|결합 방향|예시|의미|
|`left`|`a + b + c` → `(a + b) + c`|왼쪽부터 계산|
|`right`|`a = b = c` → `a = (b = c)`|오른쪽부터 계산|
|`none`|결합 불가|같은 연산자 중첩 사용 불가|

---

## ✅ 요약 정리

|   |   |
|---|---|
|항목|설명|
|사용자 연산자 선언|`infix operator +++ : MyPrecedenceGroup`|
|우선순위 그룹 정의|`precedencegroup MyPrecedenceGroup { ... }`|
|조절 가능 요소|`associativity`, `higherThan`, `lowerThan`|
|목적|계산 순서 제어 (괄호 없이도 예상된 순서대로 동작)|

---

  

끝