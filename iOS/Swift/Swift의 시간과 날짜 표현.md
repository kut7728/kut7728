### Date 타입

```Swift
let someTime = Date()

print(someTime) // 2025-01-26 13:32:44 +0000
```

- `Date(timeIntervalSinceNow: 300)` → 지금 시간으로부터 300초 후의 시간
- `Date(timeInterval: 300, since: someTime)` → someTime 으로부터 300초 후의 시간
- `print(”실행 시간: \(-someTime.timeIntervalSinceNow)”)` → someTime 부터 지금까지의 시간차이 출력

  

### DateFormatter

> [!important] Date 타입을 문자열 표현으로 변환해주는 역할
> 
> 인스턴스화 시켜 커스텀하여 사용

```Swift
let date = Date()

let dateFormatter = DateFormatter() // 인스턴스 생성
dateFormatter.dateStyle = .medium
dateFormatter.timeStyle = .medium

dateFormatter.locale = Locale(identifier: "ko_KR")
print(dateFormatter.string(from: date)) // 2021. 8. 24. 오후 8:55:52

dateFormatter.dateFormat = "YY년 M월 d일 h시 mm분 ss초"
print(dateFormatter.string(from: date)) // 21년 8월 24일 8시 55분 52초

----------------------------------------------------------------------

let dateFormatter = {
    let formatter = DateFormatter()
    formatter.dateFormat = "yyyy년 M월 d일"
    formatter.locale = Locale(identifier: "ko_KR")
    return formatter
}

...

Text("\(appoint.pickedDate, formatter: dateFormatter())")
    .font(.system(size: 14))
    .frame(maxWidth: .infinity, alignment: .leading)
```

|포맷|설명|
|---|---|
|y|연도|
|M|월|
|d|일|
|E|요일|
|a|am/pm|
|h|12시간제 시간|
|H|24시간제 시간|
|m|분|
|s|초|

  

### Calendar

> [!important] 달력과 관련된 정보를 담는 구조체
> 
> 인스턴스화 할때 identifier enum 을 통해 어떤 달력인지 전달하고
> 
> 인스턴스 후에는 달력의 요소별로 DateComponent를 얻을 수 있다

```Swift
let date = Date()
var calendar = Calendar(identifier: .gregorian)
print(calendar.dateComponents([.day, .month], from: date)) 
// month: 8 day: 25 isLeapMonth: false

var dateComponents = DateComponents()
dateComponents.year = 1995
print(calendar.date(from: dateComponents)) 
// Optional(1994-12-31 15:00:00 +0000)
```

  

### DateComponents

> [!important] 자주 사용하는 경우에는 DateComponents를 인스턴스화 시켜서 선언할 수도 있다.

```Swift
var calendar = Calendar(identifier: .gregorian) // 인스턴스 생성: 캘린더 유형 설정
let dateComponents = DateComponents(year: 2222, month: 2, day: 22) // 원하는 요소만 입력하여 날짜 추출
let myDate = calendar.date(from: dateComponents) // date타입으로 변환. 옵셔널 타입이다.

let formatter = DateFormatter() // 포맷설정을 위해 인스턴스 생성
formatter.locale = Locale(identifier: "ko_kr") // 한국 시간으로 지정
formatter.dateStyle = .full // 날짜스타일 지정
print(formatter.string(from: myDate!)) // 2222년 2월 22일 금요일
```

  

> 참고

[https://leeari95.tistory.com/30](https://leeari95.tistory.com/30)