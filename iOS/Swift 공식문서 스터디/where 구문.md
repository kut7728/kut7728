# **제네릭(Generic)에서의 where 절**

- **사용 목적 :** 타입 간 관계를 명확히 제약하고 싶을 때

```Swift
func printElements<T: Sequence>(of sequence: T) where T.Element: CustomStringConvertible {
    for element in sequence {
        print(element.description)
    }
}
```

- T는 Sequence여야 하고,
- 그 안의 Element는 CustomStringConvertible을 따를 때만 허용

  

# **패턴 매칭 (switch, if case, for case)에서 where**

## **1️⃣ switch-case에서 조건 추가**

```Swift
let number = 7

switch number {
case let x where x % 2 == 0:
    print("짝수입니다.")
default:
    print("홀수입니다.")
}
```

- where로 **case 조건을 더 세밀하게 설정**

## **2️⃣ for case let과 함께 사용**

```Swift
let results: [Result<Int, Error>] = [.success(1), .failure(NSError()), .success(2)]

for case let .success(value) in results where value > 1 {
    print("1보다 큰 성공 값: \(value)")
}
```

- case와 where를 함께 사용해 필터링 가능

  

# **프로토콜 확장에서 제약할 때**

```Swift
extension Collection where Element == Int {
    func sum() -> Int {
        return reduce(0, +)
    }
}
```

- Element가 Int인 경우에만 sum() 메서드를 사용할 수 있도록 제한

  

[https://seons-dev.tistory.com/entry/Swift-%EA%B3%A0%EA%B8%89-%EB%AC%B8%EB%B2%95-where-%EC%A0%88-%ED%8A%B9%EC%A0%95-%ED%8C%A8%ED%84%B4%EA%B3%BC-%EA%B2%B0%ED%95%A9](https://seons-dev.tistory.com/entry/Swift-%EA%B3%A0%EA%B8%89-%EB%AC%B8%EB%B2%95-where-%EC%A0%88-%ED%8A%B9%EC%A0%95-%ED%8C%A8%ED%84%B4%EA%B3%BC-%EA%B2%B0%ED%95%A9)