> [!important]
> 
> ### 간편한 이름없는 함수
> 
> 사실 함수가 이름을 붙인 클로저이다 (Named Closure)
> 
>   
> 
> > 참고
> 
> [https://babbab2.tistory.com/81](https://babbab2.tistory.com/81)
> 
> [https://babbab2.tistory.com/82?category=828998](https://babbab2.tistory.com/82?category=828998)
> 
> [https://babbab2.tistory.com/83](https://babbab2.tistory.com/83)

  

- [[#간편한 이름없는 함수]]
- [[#클로저 표현식]]
- [[#클로저 간단하게 사용하기]]
    - [[#트레일링 클로저]]
    - [[#클로저 경량 문법]]
- [[#@escaping]]

  

## 클로저 표현식

> 클로저 기본 문법

```Swift
{(parameters) -> returnType in
    statements
}

let multiply = { (a: Int, b: Int) -> Int in
    return a * b
}

print(multiply(3, 4))  // 출력: 12
```

  

> 클로저도 1급 객체의 특성을 가짐

- 1급 객체의 특성인 상수에 대입이 가능하다

```Swift
let simpleClosure = { () -> () in
    print("This is a simple closure!")
}

simpleClosure() // "This is a simple closure!" 출력
```

```Swift
let multiply = {(_ val1: Int, _ val2: Int) -> Int in
	return val1 * val2
}
let result = multiply(10, 20)
```

  

> 함수의 매개변수로 사용되는 클로저

```Swift
func performOperationWithClosure(closure: (Int, Int) -> Int) {
    let result = closure(5, 3)
    print("Result: \(result)")
}

performOperationWithClosure(closure: { (a, b) in
    return a + b
})
// "Result: 8" 출력
```

  

> **클로저 단순화**

```Swift
let multiply: (Int, Int) -> Int = {
	$0 * $1
}
```

- 암시적 반환 : 단일 표현식을 반환하는 클로저는 `return` 키워드를 생략 가능하다
- 축약 인수 이름 : 매개변수를 $0, $1 등으로 참조 가능

  

  

## 클로저 간단하게 사용하기

### 트레일링 클로저

`함수의 마지막 파라미터가 클로저`일때, `함수 뒤에 클로저를 작성하는 문법`

```Swift
func doSomething(closure: () -> ()) {
    closure()
}

doSomething(closure: { () -> () in
    print("Hello!")
})
```

```Swift
doSomething () { () -> () in
		print("Hello!")
}
```

1. 파라미터가 클로저 하나라면 호출구문인 `()` 도 생략 가능
2. 클로저가 여러개인 함수라면 마지막 하나만 트레일링 클로저로 적을 수 있고 나머지는 동일하게 호출구문 내부에 구현
3. 트레일링 클로저에서는 `closure:` 이라는 외부매개 변수 이름도 생략 가능

  

  

### 클로저 경량 문법

  

> 기본적인 클로저 사용례

```Swift
func doSomething(closure: (Int, Int, Int) -> Int) {
    closure(1, 2, 3)
}

doSomething(closure: { (a: Int, b: Int, c: Int) -> Int in
    return a + b + c
})
```

  

> 파라미터와 리턴의 타입을 생략할 수 있다!

```Swift
doSomething(closure: { (a, b, c) in
		return a + b + c
})
```

  

> 파라미터 이름 대신 단축인자(Shortand Argument Names)를 사용하여 파라미터 이름과 in키워드 삭제!

```Swift
doSomething(closure: {
		return $0 + $1 + $2
})
```

  

> 단일 리턴문만 있을 경우 return 키워드 삭제!

```Swift
doSomething(closure: {
		$0 + $1 + $2
})
```

  

> 클로저가 마지막 파라미터라면 트레일링 클로저로 작성 가능!

```Swift
doSomething() {
		$0 + $1 + $2
}
```

  

> 호출문자 () 속에 아무 내용이 없다면 생략 가능!

```Swift
doSomething {
		$0 + $1 + $2
}
```

  

## `@escaping`

> [!important] 일반적으로 파라미터로 제공받은 클로저는 해당 함수를 벗어나지 못하고 내부 실행만 가능하다
> 
> `이는 일반적인 클로저가 모두 non-escaping closure 이기 때문! (흐름을` `**탈출**``하지 못하는 클로저)`
> 
> → 클로저를 변수나 상수에 대입할 수 없고,
> 
> → 중첩함수 내부에서 매개변수로 받은 클로저를 사용할 경우 중첩함수를 리턴할 수 없다
> 
> → 함수의 실행 흐름을 탈출하지 못함. 즉, 함수 종료 전에 무조건 실행 되어야 한다.
> 
> ![[Attachments/img1.daumcdn 6.png|img1.daumcdn 6.png]]

  

> 하지만 `@escaping`을 사용하면 가능해진다!

```Swift
func doSomething(closure: @escaping () -> () ) {
		let f: () -> () = closure
}
```

  

> 만약 클로저를 옵셔널로 감싸게 된다면?

옵셔널로 감싸는 순간 클로저가 아니게 되기 때문에 non-escaping의 특성이 사라지게 됨

→ 따라서 `@escaping`을 굳이 붙이지 않아도 원했던 특성을 가질 수 있다!