ref ) [https://dvlpr-chan.tistory.com/114](https://dvlpr-chan.tistory.com/114)

---

# 순환 열거형이란?

- `순환(재귀) 열거형`은 열거형의 케이스가 연관 값으로 자신의 열거형 타입을 포함할 수 있는 열거형을 말합니다.
    - 트리구조, 계층적 데이터를 표현하는데 유용하고, 재귀적인 데이터 모델링을 가능하게 함.
- 재귀적으로 해당 열거형 케이스를 반복하게 되므로 `indirect` 키워드를 사용해 명시한다.
    - `indirect` 키워드를 사용하면 컴파일러에게 메모리 관리를 위해 적절한 `간접 참조`를 추가하도록 지시함.

이해가 안되므로 예시를 봐보도록 하자.

---

  

# 예제

```Swift
indirect enum ArithmeticExpression {
    case number(Int) //나는 숫자(정수만 들어와!)!
    case addition(ArithmeticExpression, ArithmeticExpression) 
    //나는 덧셈! + (ArithmeticExpression이라는 열거형이 모두 들어와도됨)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
    //나는 곱셈 + (ArithmeticExpression이라는 열거형이 모두 들어와도됨)
}

let expr = ArithmeticExpression.multiplication(
    .addition(.number(5), .number(4)),
    .number(2)
)


func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case .number(let value): //.number의 리턴 정의
        return value
    case .addition(let left, let right): //.addition의 리턴 정의
        return evaluate(left) + evaluate(right)
    case .multiplication(let left, let right): //.multiplication의 리턴 정의
        return evaluate(left) * evaluate(right)
    }
}

print(evaluate(expr)) // 출력: 18
```

  

엄.. 예제의 순서를 봐보도록 하자.

---

  

# 예제 순서

```Swift
print(evaluate(expr))
```

- `expr`의 값을 `evaluate` 라는 함수의 매개변수로 들어감
    - `expr`이 뭐노

```Swift
let expr = ArithmeticExpression.multiplication(
    .addition(.number(5), .number(4)),
    .number(2)
)

즉

ArithmeticExpression.multiplication(
    ArithmeticExpression.addition(
        ArithmeticExpression.number(5),
        ArithmeticExpression.number(4)
    ),
    ArithmeticExpression.number(2)
)
```

- `expr`은 `ArithmeticExpression` 열거형에서 `.addition`과 `.number`를 매개변수로 하는 `multiplication`의 반환값임
- 위 코드는 `5와 4를 더한 후 2를 곱` 해라 ㅇㅇ
- `evaluate`를 보자.

```Swift
func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case .number(let value):
        return value
    case .addition(let left, let right):
        return evaluate(left) + evaluate(right)
    case .multiplication(let left, let right):
        return evaluate(left) * evaluate(right)
    }
}
```

  

---

  

- `expr`는 `.multiplication(...)` 이니까 `switch`문에서 이쪽으로 들어감

```Swift
case .multiplication(let left, let right):
    return evaluate(left) * evaluate(right)
```

- `left`: `.addition(.number(5), .number(4))`
- `right`: `.number(2)`

  

- `left`는 `.addition(.number(5), .number(4))` 이니까

```Swift
case .addition(let left, let right):
    return evaluate(left) + evaluate(right)
```

- 여기서 또 내부로 들어감:
    - `left`: `.number(5)` → `evaluate(.number(5))` → 5 반환
    - `right`: `.number(4)` → `evaluate(.number(4))` → 4 반환

👉 따라서: `evaluate(.addition(.number(5), .number(4)))` → `5 + 4 = 9`

---

  

```Swift
let expr = ArithmeticExpression.multiplication(
    .addition(.number(5), .number(4)), // 5 + 4 = 9
    .number(2)// 2
)
```

다음 `evaluate(right)` 계산:

- `right`는 `.number(2)` → `evaluate(.number(2))` → 2 반환

  

```Swift
evaluate(expr) = evaluate(left) * evaluate(right)
               = 9 * 2
               = 18
```

- 최종 계산 → 씨팔

  

```Swift
print(evaluate(expr)) 
```

- 출력

  

  

## 트리

---

```Plain
    *
   / \\
  +   2
 / \\
5   4
```

---

  

## ✅ 최종 정리

|   |   |   |
|---|---|---|
|단계|표현식|결과|
|`evaluate(.number(5))`|5|5|
|`evaluate(.number(4))`|4|4|
|`evaluate(.addition(5, 4))`|5 + 4|9|
|`evaluate(.number(2))`|2|2|
|`evaluate(.multiplication(9, 2))`|9 * 2|18|

  

---

# 퉤