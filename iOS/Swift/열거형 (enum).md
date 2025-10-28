---
설명: 노션의 다중선택처럼 여러개의 선택지가 정해진 데이터 타입
---
> [!important] 노션의 다중선택처럼 여러개의 선택지가 정해진 데이터 타입

  

### 기본 사용예

```Swift
enum Temperature {
	case hot
	case warm
	case cold
}

func displayTempInfo(temp: Temperature) {
	switch temp {
		case .hot:
			print("it is hot.")
		case .warm:
			print("it is warm.")
		case .cold:
			print("it is cold.")
	}
}

displayTempInfo(temp: Temperature.warm)   >> it is warm.
```

  

### 원시값을 가지는 enum

```Swift
enum CompassPoint: String {
	case north = "북"
	case south = "남"
	case east = "동"
	case west = "서"
}

var direction = CompassPoint.east
let direction2 = CompassPoint(rawValue: "남")

switch direction {
	case .north:
		print(direction.rawValue)
	case .south:
		print(direction.rawValue)
	case .east:
		print(direction.rawValue)
	case .west:
		print(direction.rawValue)
}
```

- enum의 각 케이스에 대해 원시값을 설정
- rawValue 메서드를 통해 원시값 참조 가능
- 객체를 선언할때 `타입이름(rawValue: <원시값>)` 형태로 원시값을 통해서 케이스를 지정할 수도 있음

  

### 연관값을 가지는 enum

```Swift
enum PhoneError {
	case unKnown
	case batteryLow(String)
}

let error = PhoneError.batteryLow("배터리가 곧 방전됩니다.")

switch error {
case .batterLow(let message):
	print(message)
	
case .unKnown:
	print("알 수 없는 에러입니다.")
}

// 출력: 배터리가 곧 방전됩니다.
```

- 처음 객체 선언시에 연관값을 초기화 가능