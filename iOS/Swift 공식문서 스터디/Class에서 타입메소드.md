  

## ✅ 타입 메서드란?

- `클래스`, 구조체, 열거형에서 선언 가능
- **인스턴스가 아니라 타입 그 자체에 속함**
- `static` 키워드 또는 클래스에서는 `class` 키워드 사용

---

## 📌 선언 방법

### 🔹 구조체나 열거형에서는 `static`

```Swift
struct Math {
    static func square(_ x: Int) -> Int {
        return x * x
    }
}

let result = Math.square(4) // 16
```

  

---

  

### 🔹 클래스에서는 `static` 또는 `class`

```Swift
class Animal {
    static func sound() {
        print("Some sound")
    }

    class func typeDescription() {
        print("This is an animal class")
    }
}
```

- `static func ...()`: **오버라이드 불가능**
- `class func ...()`: **서브클래스에서 오버라이드 가능**

  

### 🔸 상속 예시:

```Swift
class Dog: Animal {
		//Animal Class를 상속받은 Dog 클래스
		//class func이므로 오버라이드 ㅆㄱㄴ.
		
    override class func typeDescription() {
        print("This is a dog class")
    }
}

Dog.typeDescription() 
// This is a dog class

Animal.typeDescription() 
// This is an animal class
```

---

## 🧠 인스턴스 메서드 vs 타입 메서드

|   |   |   |
|---|---|---|
|구분|인스턴스 메서드|타입 메서드|
|정의 키워드|`func`|`static func` or `class func`|
|호출 방법|`instance.method()`|`TypeName.method()`|
|예시|`dog.bark()`|`Dog.typeDescription()`|