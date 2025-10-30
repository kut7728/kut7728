---
상위 항목:
  - "[[iOS/Swift/데이터 타입]]"
---
## Swift의 세 컬렉션 - Array, Dictionary, Set

- Collection 에 객체와 값 둘다 저장 가능
- 하나의 Collection 에는 하나의 data type 만 저장 가능
    - 하지만 `any` 데이터 타입으로 생성하면 다른 데이터 타입도 혼용 가능
- `let var` 키워드로 가변성 지정

  

### 배열 - Array

> 배열 생성

```Swift
var priceArray = [Float]()   
var priceArray2: [Float]      // 빈 배열 생성

var treeArray: [String] = ['pine', 'oak', 'yew']   // 타입 지정하여 배열 생성

var nameArray = [String] (repeating: 'my string', count: 18)
// my String 이라는 문자열 10개를 가진 배열 생성
```

  

> 수정 / 조회 메소드

```Swift
treeArray.append("redwood")
treeArray += ["redwood"]    // 배열에 항목 추가하는 두가지 방법

treeArray.insert("maple", at:0)   // 배열 첫번째 위치에 maple 삽입

treeArray.count    // 항목 갯수 출력 (int)
treeArray.isEmpty    // 항목 존재 여부 출력 (boolean)

treeArray[0]
treeArray.first    // 둘다 배열의 첫번째 원소를 출력하지만 후자는 옵셔널로 안전하게 출력
```

  

> 삭제 메소드

```Swift
treeArray.remove(at: 2)   // 배열 세번째 위치 항목 삭제

treeArray.removeAll()    // 배열의 모든 항목 삭제, 빈 배열만 남음

treeArray.removeLast()   // 마지막 항목 삭제
```

  

> 기타 메소드

```Swift
let shuffledTrees = treeArray.shuffled()   // 항목 무작위로 섞기

let randomTree = treeArray.randomElement()   // 무작위 추출

treeArray.reverse()   // 원본의 항목 순서 거꾸로 변경
treeArray.reversed()   // 원본은 그대로, 순서 거꾸로된 복사본 생성

treeArray.sort()   // 항목을 오름차순으로 정렬
```

  

> 타입이 혼합된 배열

```Swift
let mixedArray: [Any] = ['A string', 432, 23.112]
```

- 이후 쓰임새에 따라 형변환이 필요할 수 있다.

  

  

### 딕셔너리 - Dictionary

> 딕셔너리 생성

```Swift
var testArray [String : String] = ["smthing" : "smthing"]

var emptyArray [String : String] = [ : ]
var emptyArray = [String : String]()

// 시퀸스 기반의 딕셔너리 초기화
let bookDict = Dictionary(uniqueKeysWithValues: zip(keys, values))
let bookDict = Dictionary(uniqueKeysWithValues: zip(1..., values))
```

  

> 딕셔너리 요소 추가, 수정 및 삭제

```Swift
var dict = ["name": "John"]
dict["phone"] = "123-456-7890" // 추가: ["name": "John", "phone": "123-456-7890"]
dict["name"] = "Alice" // 수정: ["name": "Alice", "phone": "123-456-7890"]

var dict = ["name": "John", "phone": "123-456-7890"]
dict.removeValue(forKey: "phone") // 결과: ["name": "John"]
```

  

> 딕셔너리 값 검색

```Swift
let person = ["name": "John", "age": "25"]
if let name = person["name"] {
    print("이름: \(name)") // 출력: 이름: John
}
```