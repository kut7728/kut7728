---
설명: 개요, 언랩핑, nil병합 연산자
상위 항목:
  - "[[iOS/Swift/데이터 타입]]"
---
> [!important] 변수 또는 상수에 값이 할당되지 않은 상황을 처리하기 위한 타입

  

## Optional Type

값이 있을지 없을지 확실하지 않을때 사용되는 타입 ex) 키값으로 딕셔내리 참조

```Swift
let stock: Int?
let stock: Int? = nil
let stock: Optional<Int> = nil    -> 셋 모두 동일

stock = 123

print(stock)
>>> Optional(123)
```

- `nil` = 값이 없다는 뜻
- 하지만 타입 추론을 위해 타입이름은 적되 `?` 를 뒤에 붙임
- 이후에 값을 지정하고 출력해보면 `Optional(123)` 이런식으로 포장되어있음 → `Unwrapping` 필요

  

### Optional Chaining

옵셔널로 되어있는, nil일지도 모르는 프로퍼티, 메서드, 서브스크립션 등을 가져오거나 호출할때 사용하는 ? 문법

```Swift
struct Developer {
	let name: String
}

struct Company {
	let name: String
	var developer: Developer?
}

let developer = Developer(name: "kim")
var myCompany = Company(name: "naver", developer: developer)

print(myCompany.developer?.name)  // 출력: Optional("kim")
```

- Company 구조체의 developer 프로퍼티는 옵셔널 타입이므로 참조할때도 ? 를 붙여서 참조
- 옵셔널 체이닝을 통해 참조한 값은 옵셔널임으로 적절한 언랩핑 필요

  

## Unwrapping

==**: 값 추출하기**==

> 강제추출

```Swift
print(stock!)
	>> 123
```

- `!` 를 붙여 강제로 언랩핑 하는 방법, 하지만 실사용은 안하는 편
- 값이 지정되지 않은 옵셔널 타입을 강제추출하면 fatal error 뜸

  

> **Optional Binding**

```Swift
if let [name] = [Optionalname] {
	statements
} //else 도 사용 가능

while let [name] = [Optionalname] {
	statements
}

guard let [name] = [Optionalname] else { return }
statements
```

- `Optionalname` 에 값이 저장되어 있는 경우, `Unwrapping` 되어 `name`에 선언이 되고 구문 실행
- Optional Binding으로 선언된 `if`, `while` 의 상수는 해당 스코프 내에서만 사용 가능  
    하지만 `guard` 는 상위 스코프에서 접근 가능, else 구문에서는 접근 불가능
- `let` 대신 `var` 도 가능

> [!important]
> 
> > _==example==_
> 
> ```Swift
> var num :Int? = 123
> 
> if let n = num {
> 	print(num)
> }
> ```

> [!important]
> 
> ### 이름이 같다면?
> 
> ```Swift
> var num :Int? = 123
> 
> guard let num = self.num else { return }
> 
> or
> 
> guard let num else { return }
> ```

- 선언하는 변수와 참조하는 변수가 이름이 같다면 등호 생략 가능

  

> **nil 병합 연산자**

nil 값일 경우 디폴트 값을 사용하도록 해줌

```Swift
let customerName: String? 
print("welcome back, \(customerName ?? "customer")")
```