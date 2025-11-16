## Static

> [!important] Class 선언시에 메소드나 프로퍼티 앞에 붙이는 키워드
> 
> 인스턴스화 시키지 않아도 접근할 수 있다!

  

## Singleton

> [!important] 여러 곳에서 쓰이는 Class의 객체들이 동일한 데이터를 갖고 있길 바랄때 사용하는 방법

```Swift
class Dog {
	var name = "멍멍이"
	static let shared = Dog()
}

let dog1 = Dog.shared
dog1.name = "야옹이"

let dog2 = Dog.shared
print(dog2.name)   // "야옹이"
```