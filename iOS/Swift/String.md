---
상위 항목:
  - "[[데이터 타입]]"
---
- 목차
    - [[#MultipleLine String]]
    - [[#String]]
        - [[#NSString 과 String]]
        - [[#문자열의 가변성 (Mutability)]]
        - [[#String Interpolation (문자열 보간)]]
        - [[#문자열 포맷]]
        - [[#탈출문자 출력방법]]
    - [[#String Index]]
    - [[#String 생성]]
        - [[#문자열은 배열과 같다!]]
    - [[#String 편집]]
        - [[#Append 와 Appending]]
        - [[#문자열 중간에 삽입]]
        - [[#문자열 대체]]
        - [[#문자열 삭제]]

## MultipleLine String

```Swift
let multipleLine = """
the last symbol decides where the paragraph starts.
so final symbol must place right than the
start position of the paragraph.
"""
```

- 마지막 따옴표의 위치는 무조건 문장의 가장 왼쪽과 같아야 함
- 따옴표 내부에 `역슬래쉬 \` 는 줄 바꿈을 무효시킴

  

## String

### NSString 과 String

- 일반 String은 Swift String이라고 부름
- 둘이 서로 자동 변환은 안됨, 타입 캐스팅 필요  
    `let swiftStr: String = nsstr as String`
- 그냥 일반 String 쓰면 됨

  

### 문자열의 가변성 (Mutability)

- 문자열의 뒤에 문자열을 추가해주는 메소드 ( `.append()` )는  
    문자열이 상수로 선언되면 사용할 수 없다.
    
      
    

### String Interpolation (문자열 보간)

```Swift
let size = 56.78
var str = String(size) + "KB"
var str = "\(size)KB"
```

- 문자열의 중간에 표현식을 사용할 수 있게 해준다.

  

### 문자열 포맷

```Swift
String(format : "%.5fKB", size)
	>> 56.78000KB
String(format : "%010.3f")
	>> 000056.780
```

- %f : 실수 대체  
    %.3f - 소수 3자리까지 출력  
    %10.3f - 전체 자릿수를 10자리 출력, 그중 소수는 3자리 (점도 한자리 차지)  
    %010.3f - 전체 자릿수 10, 소수 3자리, 빈자리를 0으로 채움  
    %d : 정수 대체  
    %@ : 문자열 대체  
    %- : 숫자를 왼쪽으로 정렬
- % 문자 추가하려면 %% 입력
    
      
    

### 탈출문자 출력방법

```Swift
print("\"Hello, He said.\"")
print(#""Hello", He said.""#)
```

- \#” “# 브라켓을 사용하면 내부의 문자열은 Raw String이 됨
    - 굳이 Escape Sequence 사용 안해도 됨
- Raw String 내부에서 Escape Sequence 쓰려면 역슬래쉬 뒤에 샵 붙이기  
    `#””Hello” \#n He said.””#`

  

## String Index

> [!important] Swift 에서는 String의 인덱스가 정수형이 아님! (ㅅㅂ!)
> 
>   
> 왜?? 유니코드 처리를 간편하게 하기 위해서…

```Swift
let str = "Swift"
str.startIndex

let firstCh = str[str.startIndex]
print(firstCh)
	>> S 

let lastCharIndex = str.index(before: str.endIndex)
let lastCh = str[lastCharIndex]
print(lastCh)
	>> t
```

- 문자열의 첫 글자의 인덱스는 `.startIndex`  
    문자열의 끝 글자의 인덱스는 `str.index(before: str.endIndex)` 두번째 글자의 인덱스는 `str.index(after: str.startIndex)` 세번째 글자의 인덱스는 `str.index(str.startIndex, offsetBy: 2)`  
    혹은 `str.index(str.endIndex, offsetBy: -3)`
- `.endIndex` 는 마지막 글자의 다음 인덱스를 불러옴

  

## String 생성

```Swift
var str = "Hello, Swift String"
var emptyStr = ""
emptyStr = String()
```

- `String()` 은 생성자, 함수와 비슷하지만 키워드 대신 데이터 타입이 들어감

```Swift
let hex = String(123, radix: 16)

let repeatStr = String(repeating: "y", count: 7)

str.lowercased()
str.uppercased()
str.capitalized() //ed로 끝나는 메소드는 원본은 납두고 새로운 결과를 리턴
```

- `radix` 파라미터에 16 넣으면 16진수, 8넣으면 8진수로 문자열 생성

### 문자열은 배열과 같다!

```Swift
let num - "1234567890"
num.randomElement() >> "4"
num.shuffled() >> ["4", "5", "2", "7" ... ]

string(num.shuffled()) >> "4527..."
```

  

## String 편집

### Append 와 Appending

```Swift
var str = "Hello"
str.append(", ")
str  >> "Hello, "

let s = str.appending("Swift")
str  >> "Hello, "
s  >> "Hello, Swift"
```

- `.append()` 는 str(원본)에 직접 추가 → 대상이 상수면 에러 남  
    `.appending()` 은 str의 복사본에 추가하고 복사본을 리턴

  

### 문자열 중간에 삽입

```Swift
var str = "Hello Swift"
str.insert(", ", at: str.index(str.startIndex, offsetBy: 5))
```

- `대상이름.insert(contentsOf: 추가할 문자열, at: 추가할 대상의 인덱스)`

  

### 문자열 대체

```Swift
var str = "Hello, Objective-C"

if let range = str.range(of: "Objective-C") {
	str.replaceSubrange(range, with: "Swift")
}
```

- `.replaceSubrange()` 는 원본에 직접 편집  
    `.replacingCharacters()` 는 복사본에 편집하고 리턴
- `.replacingOccurrences(of: , with: )` 는 문자열 탐색과 변경을 함께 수행해줌, ing임으로 복사본에 작업, 탐색결과 없으면 원본 리턴  
    파라미터로 `options: [.caseInsensitive]` 를 넣으면 대소문자 무시

  

### 문자열 삭제

```Swift
var str = "Hello, Awesome Swift!!!"

let lastCharIndex = str.index(before: str.endIndex)
var removed = str.remove(at: lastCharIndex)
removed  >> !
str  >> "Hello, Awesome Swift!!"

var removed2 = str.removeFirst()
removed2  >> H
str  >> "ello, Awesome Swift!!"
```

- `.remove` 계열 메소드는 모두 삭제되는 문자(Character)를 리턴
- `.removeFirst()`는 앞에서부터 한 문자씩 삭제, 파라미터로 갯수 입력 가능
- `.removeLast()` 는 뒤에서부터
- `.removeSubrange()` 는 원본에서 입력된 인덱스 만큼을 지움
- `.removeAll()` 는 대상의 문자열을 모두 삭제
- `.dropLast()` 는 대상의 뒤에서부터 갯수만큼 빼고 리턴