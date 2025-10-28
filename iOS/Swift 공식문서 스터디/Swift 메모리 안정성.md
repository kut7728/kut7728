  

[https://bbiguduk.gitbook.io/swift/language-guide-1/memory-safety](https://bbiguduk.gitbook.io/swift/language-guide-1/memory-safety)

  

# 메모리에 충돌하는 접근이란?

- 다른 코드가 같은시간에 같은 위치의 메모리에 접근할 때 발생 가능

  

## 충돌 가능한 메모리 접근의 특징

1. 두 접근이 모두 쓰기중이고, atomic인 경우
2. 메모리의 같은 위치에 접근하는 경우
3. 접근하는 시간이 겹치는 경우

  

## 종류

### In-Out 파라미터에 충돌 접근

  

### 메서드에서 self에 충돌 접근

```Swift
extension Player {
    mutating func shareHealth(with teammate: inout Player) {
        balance(&teammate.health, &health)
    }
}

var oscar = Player(name: "Oscar", health: 10, energy: 10)
var maria = Player(name: "Maria", health: 5, energy: 10)
oscar.shareHealth(with: &maria)  // OK
```

- 같은 인스턴스에 중복 접근시 충돌

### 프로퍼티에서 충돌 접근

- 값 타입인 구조체, 튜플, 열거형의 프로퍼티를 수정하는 것은 값의 전체 변경을 야기함
- 따라서 튜플의 요소에 쓰기 접근이 겹치면 충돌이 일어남
    
    ```Swift
    var holly = Player(name: "Holly", health: 10, energy: 10)
    balance(&holly.health, &holly.energy)  // Error
    ```
    
    - 근데 또 지역변수로 바꾸면 가능하다고 함…?? Tqlkf…..
    
    ```Swift
    func someFunction() {
        var oscar = Player(name: "Oscar", health: 10, energy: 10)
        balance(&oscar.health, &oscar.energy)  // OK
    }
    ```