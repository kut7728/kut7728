> [!important] 리턴되는 값의 타입을 미정으로 해줌

  

```Swift
func testFunc() -> Array<Int> {
    return [1, 2, 3]
}

func testFunc() -> some Collection {
    return [1, 2, 3]
}

func testFunc() -> some Collection {
    return ["a": 1, "b": 2, "c": 3]
}
```

- 처음에는 배열을 출력하려는게 확실해서 타입을 명확하게 지명했지만
- 리턴값이 달라질 수 있을때는 some을 붙이면서 미정된 타입이라고 알려줌

  

  

- 만약 SwiftUI에서 some을 안 쓴다면 매번 함수 리턴값을 VStack, HStack, Button, Text 등등 구체적인 뷰값을 명시해줘야해서 아주 귀찮았을 것.