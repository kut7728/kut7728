---
설명: 클래스 속 프로퍼티로 리턴값 만들어놓기
---
> [!important] 매개변수로 성과 이름을 받고 풀네임을 리턴하는 기능을 넣고자 하는 방법은 두가지이다.

```Swift
class Person {
	let lastName: String
	let firstName: String
	
	init(lastName: String, firstName: String) {
		self.lastName = lastName
		self.firstName = firstName
	}
	
	func fullName() -> String {
		return lastName + firstName
	}
	
=====================

let person = Person(lastName: "김", firstName: "엘사")
print(person.fullName())
```

```Swift
class Person {
	// Stored Property
	let lastName: String
	let firstName: String
	
	// Computed Property
	var fullName: String {
		return firstName + lastName
	}
	
	init(lastName: String, firstName: String) {
		self.lastName = lastName
		self.firstName = firstName
	}
	
=====================

let person = Person(lastName: "김", firstName: 엘사")
print(person.fullName)
```