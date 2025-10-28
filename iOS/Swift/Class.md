- 목차
    
    - [[#Class 의 생성]]
    - [[#Class의 Object (Instance) 생성]]
    - [[#init 을 통한 초기화]]
    - [[#상속 (Inheritance)]]
    - [[#Class는 레퍼런스 타입이다]]
    
    ---
    

  

## Class 의 생성

```Swift
class Student {
  var name = ""
  var year = 0
  var gpa = 0.0
  var honors = false
}
```

  

## Class의 Object (Instance) 생성

```Swift
var ferris = Student()

ferris.name = "Ferris Bueller"
ferris.year = 12
ferris.gpa = 3.81
ferris.honors = false
```

  

## init 을 통한 초기화

```Swift
class Student {
  var name = ""
  var year = 0
  var gpa = 0.0
  var honors = false
  
  init(name: String, year: Int, gpa: Double, honors: Bool) {
	  self.name = name
	  self.year = year
	  self.gpa = gpa
	  self.honors = honors
  }
}

var ferris = Student(name: "Ferris Bueller", year: 12, gpa: 3.81, honors: false)
```

- init 없이도 argument 초기화 가능하지만 협업 시인성 향상을 위해서라도 사용
- property 의 선언 순서에 맞춰서 parameter 적어야 함

  

  

  

## 상속 (Inheritance)

> [!important] Structure 와 다른점! 다른 Class의 property, method 등을 받아 올 수 있다!!

  

### 상속 받는 Class 생성하기

```Swift
class Subclass: Superclass {

}
```

- 제공하는 Class는 SuperClass 받는 Class 는 SubClass 라고 부름
- SubClass는 SuperClass 의 property, method를 전부 포함하고 자기고유한 거시기도 가지고 있다.

  

### Overriding Methods

```Swift
class BankAccount {
  var balance = 0.0

  func deposit(amount: Double) {
    balance += amount
  }

  func withdraw(amount: Double) {
    balance -= amount
  }
}

class SavingsAccount: BankAccount {
  var interest = 0.0
  var numWithdraw = 0

  func addInterest() {
    let interest = balance * 0.01
    self.deposit(amount: interest)
  }

  override func withdraw(amount: Double) {
    balance -= amount
    numWithdraw += 1
  }
}
```

- BankAccount Class를 상속받되 withdraw() 메소드는 Override를 통해 고유한 메소드로 만듬
- override 하는 메소드는 부모 메소드의 **파라미터 갯수와 타입이 같아야** 하고 **반환하는 타입도 일치해야** 한다.
- Override 키워드를 통해 컴파일러에게 고지
- init 은 overriding 불가
- override 후에 부모 메소드를 사용하고 싶다면 `super.<메소드이름>` 으로 사용 가능하다.

  

### init 의 override

```Swift
class Student {
  var name = ""
  var year = 0
  var gpa = 0.0
  var honors = false
  
  init(name: String, year: Int, gpa: Double, honors: Bool) {
	  self.name = name
	  self.year = year
	  self.gpa = gpa
	  self.honors = honors
  }
}

class SpecialStudent: Student {
	var exceptional = true
	
	init(name: String, year: Int, gpa: Double, honors: Bool, exceptional: Bool) {
	  self.exceptional = exceptional
	  super.init(name: name, year: year, gpa: gpa, honors: honors)
  }
}
```

- SubClass 고유 property를 포함하는 init을 만들 때 Superclass 의 init을 super.init 을 통해 참조해야한다.

  

  

## Class는 레퍼런스 타입이다

- Structure는 Value 타입이지만, Class는 Reference 타입이다.
- Value 타입은 원본을 놔두고 복사본을 변수에 할당하지만  
    Class 타입은 원본을 변수에 할당하게 된다.
- 따라서 Class 인스턴스 A를 다른 변수 B에 할당하면, B를 수정할때 A역시 함께 수정된다.