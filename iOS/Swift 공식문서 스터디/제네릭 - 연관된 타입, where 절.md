  

# 제네릭(Generic)

제네릭은 함수, 타입(구조체, 클래스, 열거형 등)에서 타입을 유연하게 지정할 수 있게 해주는 swift의 기능이다.

즉 코드 작성시 `구체적인 타입`을 명시하지 않고, 실제 사용할 때 `타입을 지정해줘` 코드의 재사용성과 `확장성`이 높아짐.

```Swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temp = a
    a = b
    b = temp
}
```

여기서 `T`는 타입의 `placeholder`임.

함수가 호출될 때? 실제 타입이 결정됨ㅇㅇ

  

예시 1: Int 타입 값 교환

```Swift
var num1 = 10
var num2 = 20

swapTwoValues(&num1, &num2)

print("num1: \(num1), num2: \(num2)") // 출력: num1: 20, num2: 10
```

  

예시 2: String 타입 값 교환

```Swift
var str1 = "Hello"
var str2 = "World"

swapTwoValues(&str1, &str2)

print("str1: \(str1), str2: \(str2)") // 출력: str1: World, str2: Hello
```

  

예시 3: Double 타입 값 교환

```Swift
var d1 = 3.14
var d2 = 2.71

swapTwoValues(&d1, &d2)

print("d1: \(d1), d2: \(d2)") // 출력: d1: 2.71, d2: 3.14
```

  

참고

함수의 파라미터 앞에 `&`를 붙여서 `inout 파라미터임`을 명시해야 함

---

  

# 연관된 타입(Associated Type)

연관된 타입은 프로토콜에서 사용하는 `제네릭 개념`임.

프로토콜을 정의할때, `프로토콜을 채택하는 타입`이 나중에 구체적으로 지정할 수 있는 타입의 `placeholder`를 선언 가능ㅇㅇ

  

이때 `associatedtype` 키워드를 사용함

```Swift
protocol Container {
    associatedtype Item //네년의 자료형이 정확하게 뭔지 모르겠는데 너 쓸거 같으니 정의는 해야댐ㅇㅇ
    var items: [Item] { get set }
    mutating func append(_ item: Item)
    mutating func pop() -> Item
    var count: Int { get }
}
```

- 이 Container 프로토콜은 Item이라는 연관된 타입을 가짐.
- 이 프토토콜을 채택하는 타입(구조체, 클래스)은 Item이 어떤 타입인지 지정해야함ㅇㅇ

  

---

Int 타입을 저장하는 Stack

```Swift
struct IntStack: Container {
    // Item은 Int로 자동 추론됨
    var items = [Int]()
    
    mutating func append(_ item: Int) {
        items.append(item)
    }
    
    mutating func pop() -> Int {
        return items.removeLast()
    }
    
    var count: Int {
        return items.count
    }
}
```

예시

```Swift
var intStack = IntStack()
intStack.append(10)
intStack.append(20)
print(intStack.items) // [10, 20]
print(intStack.pop()) // 20
print(intStack.count) // 1
```

---

  

제네릭 Stack (어떤 타입이든 저장 가능)

```Swift
struct Stack<T>: Container {
    // Item은 T로 추론됨
    var items = [T]()
    
    mutating func append(_ item: T) {
        items.append(item)
    }
    
    mutating func pop() -> T {
        return items.removeLast()
    }
    
    var count: Int {
        return items.count
    }
}
```

예시

```Swift
var stringStack = Stack<String>()
stringStack.append("apple")
stringStack.append("banana")
print(stringStack.items) // ["apple", "banana"]
print(stringStack.pop()) // "banana"
print(stringStack.count) // 1
```

  

---

# Where절

`where` 절은 제네릭 타입, 함수, 프로토콜 확장 등에서 타입 파라미터나 연관된 타입에 `추가적인 제약 조건`을 줄 때 사용함.

`<T: SomeProtocol>`처럼 간단한 제약은 타입 파라미터 선언부에서 바로 쓸 수 있지만,

`where` 절을 사용하면 더 복잡한 조건(예: 연관 타입의 제약, 여러 타입 간의 관계 등)을 명확하게 지정할 수 있음.

  

예시 1: 함수에서 where 절 사용

```Swift
func printEqualElements<T>(array: [T], value: T) where T: Equatable {
    for element in array where element == value {
        print("Matching element found: \(element)")
    }
}
```

여기서 `T: Equatable`은 `T`가 `Equatable`을 준수해야 함을 명시합니다.

  
예시 2: 프로토콜 확장에서 where 절 사용

```Swift
protocol Container {
    associatedtype Item
    func contains(item: Item) -> Bool
}

extension Container where Item: Equatable { //확장을 where을 통해 조건부로 걸어줌.
    func contains(item: Item) -> Bool {
        // Item이 Equatable일 때만 사용 가능
        return false
    }
}
```

이렇게 하면 `Item`이 `Equatable`을 준수하는 경우에만 해당 확장 메서드를 사용할 수 있습니다.

  

예시 3: 여러 타입 및 연관 타입 제약

```Swift
func popAllAndTestMatch<C1: Container, C2: Container>(
    _ someContainer: inout C1,
    _ anotherContainer: inout C2
) -> Bool where C1.Item == C2.Item, C1.Item: Equatable {
    if someContainer.count != anotherContainer.count { return false }
    for _ in 0..<someContainer.count {
        if someContainer.pop() != anotherContainer.pop() { return false }
    }
    return true
}
```

여기서 `C1.Item == C2.Item, C1.Item: Equatable`은 두 컨테이너의 아이템 타입이 같고, 그 타입이 `Equatable`을 준수해야 함을 의미합니다.

  

  

![[스크린샷_2025-04-15_오후_1.19.10.png]]

핵심 요약

- 제네릭은 타입을 유연하게, 연관된 타입은 프로토콜에서 타입의 플레이스홀더 역할, where 절은 제네릭/연관 타입에 추가 제약을 줄 때 사용합니다.
- where 절은 특히 연관 타입의 제약, 여러 타입 간의 관계 등 복잡한 조건을 명확하게 표현할 때 매우 유용합니다