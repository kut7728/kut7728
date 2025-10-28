---

  

- `@PropertyWrapper`
    - `**속성의 저장 및 접근 방식을 커스터마이징**` 할 수 있게 해주는 기능. 간단히 말하면, `프로퍼티의``**값을 설정하거나 가져올 때의 로직**``을 따로 빼서` 재사용할 수 있게 해주는 구조체/클래스를 만드는 것

  

## 구현 예제

- 12이거나 작거나 ㅇㅇ

```Swift
@propertyWrapper
struct TwelveOrLess {
    private var number = 0

    var wrappedValue: Int {
        get { number }
        set { number = min(newValue, 12) } 
        // number를 갖고와서 12보다 크면 무조건 12로 set. 아니면 작은값ㅇㅇ
    }

    init() { }

    init(wrappedValue: Int) {
        self.wrappedValue = wrappedValue
    }
}
```

  

## 사용 예제

```Swift
struct SomeStruct {
    @TwelveOrLess var height: Int //이렇게 사용
}

var s = SomeStruct(height: 10)
print(s.height) // 10은 12보다 작으니 10 출력

s.height = 24 
print(s.height) // 24는 12보다 크니까 12로 출력
```

끝