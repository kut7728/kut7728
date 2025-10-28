> [!important] **타입이 구현해야 하는 요구사항을 정의한다!**
> 
> [https://bbiguduk.gitbook.io/swift/language-guide-1/protocols](https://bbiguduk.gitbook.io/swift/language-guide-1/protocols)

  

# 개요

- 메서드, 프로퍼티 등등의 요구사항을 정의할 수 있다.
- 클래스, 구조체, 열거형들이 채택할 수 있고
- 프로토콜의 모든 요구사항을 충족하면 **준수(Conform)**했다고 한다

  

# 구조

## 프로토콜 구문

```Swift
class SomeClass: SomeSuperclass, FirstProtocol, AnotherProtocol {
    // class definition goes here
}
```

- 상속하는 클래스가 있다면 프로토콜보다 먼저…
- 프로토콜은 여러개 채택 가능…

  

## 프로퍼티 요구사항

```Swift
protocol SomeProtocol {
		var mustBeSettable: Int { get set }
		var doesNotNeedToBeSettable: Int { get }
		static var someTypeProperty: Int { get set }
}
```

- 읽기전용이더라도 getter 반드시 써야한다캄

## 메서드 요구사항

```Swift
protocol RandomNumberGenerator {
    func random() -> Double
}
```

  

## 초기화 구문 요구사항

```Swift
protocol SomeProtocol {
		init(someParameter: Int)
}
```

```Swift
class SomeClass: SomeProtocol {
    required init(someParameter: Int) {
        // initializer implementation goes here
    }
}
```

- 구조체, 열거형, final 클래스의 경우 required 키워드는 필요 없음
    
    > [!important] **🔍 왜 required가 필요할까?**
    > 
    > 클래스에서 프로토콜의 init을 구현할 때 required를 붙이는 이유는 **서브클래스도 해당 초기화를 구현해야 함을 강제하기 위해서**
    > 
    > 즉, **동적 디스패치를 위한 안전 장치로 required를 요구**하는 것.
    > 
    > > “이 init은 꼭 서브클래스에서 이어받아야 하고,  
    > > 나중에 이걸 호출할 수 있도록 런타임에 대비해 둬!”
    
    > [!important]
    > 
    > ### ⚠️ 필수 초기화 구문 (Required Initializers)
    > 
    > `required` 붙여 클래스의 모든 하위 클래스가 해당 초기화 구문을 구현해야 함을 나타냅니다
    > 
    > ```Swift
    > class SomeClass {
    >     required init() {
    >         // initializer implementation goes here
    >     }
    > }
    > ```
    > 
    > 또한 초기화 구문 요구사항이 추가 하위 클래스에 적용됨을 나타내기 위해 `required` 키워드 필수, 재정의 할 때도 `override` 대신 `required` 사용 (Required override 도 가능)
    > 
    > ```Swift
    > class SomeSubclass: SomeClass {
    >     required init() {
    >         // subclass implementation of the required initializer goes here
    >     }
    > }
    > ```
    > 
    > > 부모 클래스에 필수 초기화 구문이 구현되어있다면 자식 클래스에서는 반드시 구현할 필요는 없음
    
    > [!important] **🔍  동적 디스패치?**
    > 
    > **어떤 메서드나 초기화 구문을 실행할지 런타임에 결정하는 방식**
    > 
    >   
    > 
    > Ex) 상속 관계에서 부모와 자식이 같은 메서드를 다르게 구현하면, 프로그램은 실제로 어떤 메서드를 호출해야 할지 **실행 중에(런타임에)** 결정해야 함 → `동적 디스패치`
    

  

# 프로토콜을 타입으로 사용하기

## 제네릭의 제약으로 프로토콜 사용

```Swift
protocol Drawable {
    func draw()
}

func render<T: Drawable>(_ thing: T) {
    thing.draw()
}
```

- 호출자가 T의 실제 타입을 전달
- 프로토콜을 준수하는 모든 타입을 사용 가능하면서도 컴파일시 타입이 결정됨
- thing은 실제타입이 뭔지 알기 때문에 타입의 모든 기능 사용 가능 (결국 런타임 캐스팅은 해야하지만…)

## 불투명한 타입

```Swift
func makeShape() -> some Drawable {
    return Circle()
}
```

- 반환타입은 숨기되, 프로토콜은 만족하도록
- API사용자에게 구현 세부사항을 감춤 → 추상화

## 박스형 프로토콜 타입???

```Swift
func renderAnything(_ thing: any Drawable) {
    thing.draw()
}
```

- 프로토콜을 준수하는 모든 타입에서 동작
- 타입이 런타임에 결정되는 방식, 컴파일시에는 타입을 알 수 없음
- 타입 정보가 숨겨짐 → thing은 오직 프로토콜에 선언된 멤버만 접근 가능
- 타입 고유 기능을 쓰려면 런타임 캐스팅이 필요함

  

# 위임 (Delegation)

- 클래스 또는 구조체가 책임의 일부를 다른 타입의 인스턴스에 넘겨주거나 위임할 수 있도록 하는 디자인 패턴
- 위임된 기능을 제공하기 위해 캡슐화된 프로토콜을 정의하여 구현함

- 예제 코드
    
    ```Swift
    class DiceGame {
        let sides: Int
        let generator = LinearCongruentialGenerator()
        weak var delegate: Delegate?
    
        init(sides: Int) {
            self.sides = sides
        }
    
        func roll() -> Int {
            return Int(generator.random() * Double(sides)) + 1
        }
    
        func play(rounds: Int) {
            delegate?.gameDidStart(self)
            for round in 1...rounds {
                let player1 = roll()
                let player2 = roll()
                if player1 == player2 {
                    delegate?.game(self, didEndRound: round, winner: nil)
                } else if player1 > player2 {
                    delegate?.game(self, didEndRound: round, winner: 1)
                } else {
                    delegate?.game(self, didEndRound: round, winner: 2)
                }
            }
            delegate?.gameDidEnd(self)
        }
    
        protocol Delegate: AnyObject {
            func gameDidStart(_ game: DiceGame)
            func game(_ game: DiceGame, didEndRound round: Int, winner: Int?)
            func gameDidEnd(_ game: DiceGame)
        }
    }
    ```
    
    ```Swift
    class DiceGameTracker: DiceGame.Delegate {
        var playerScore1 = 0
        var playerScore2 = 0
        
        func gameDidStart(_ game: DiceGame) {
            print("Started a new game")
            playerScore1 = 0
            playerScore2 = 0
        }
        func game(_ game: DiceGame, didEndRound round: Int, winner: Int?) {
            switch winner {
                case 1:
                    playerScore1 += 1
                    print("Player 1 won round \(round)")
                case 2: playerScore2 += 1
                    print("Player 2 won round \(round)")
                default:
                    print("The round was a draw")
            }
        }
        func gameDidEnd(_ game: DiceGame) {
            if playerScore1 == playerScore2 {
                print("The game ended in a draw.")
            } else if playerScore1 > playerScore2 {
                print("Player 1 won!")
            } else {
                print("Player 2 won!")
            }
        }
    }
    ```
    
    ```Swift
    let tracker = DiceGameTracker()
    let game = DiceGame(sides: 6)
    game.delegate = tracker
    game.play(rounds: 3)
    // Started a new game
    // Player 2 won round 1
    // Player 2 won round 2
    // Player 1 won round 3
    // Player 2 won!
    ```
    

> [!important] **❓ 그래서 델리게이션은 왜 써야하는건데요?**
> 
> > 책임분리와 확장성을 위해서
> 
> ---
> 
> 1. 기능을 외부로 위임하여 책임을 분리
> 2. 게임 로직 건드릴 필요없이 델리게이트 프로토콜을 수정할 수 있다.
> 3. 테스트가 용이함

  

# 확장과 프로토콜

## 조건적으로 프로토콜 준수

- 일반 타입에서 특정 조건에 따라 프로토콜을 준수하도록 할 수 있음
    
    ```Swift
    extension Array: TextRepresentable where Element: TextRepresentable {
        var textualDescription: String {
            let itemsAsText = self.map { $0.textualDescription }
            return "[" + itemsAsText.joined(separator: ", ") + "]"
        }
    }
    let myDice = [d6, d12]
    print(myDice.textualDescription)
    // Prints "[A 6-sided dice, A 12-sided dice]"
    ```
    
    - 요소가 TextRepresentable을 준수하면 해당 배열도 준수하도록 함

## 확장으로 프로토콜 채택 선언

- 이미 프로토콜의 요구사항을 준수하지만 채택 선언만 안되어 있는 경우
- 확장을 통해 선언해주면 평범하게 채택된채로 사용 가능
    
    ```Swift
    struct Hamster {
        var name: String
        var textualDescription: String {
            return "A hamster named \(name)"
        }
    }
    extension Hamster: TextRepresentable {}
    ```
    

  

# 클래스 전용 프로토콜

- 프로토콜의 상속 리스트에 AnyObject 프로토콜을 추가하여
- 오직 클래스에서만 채택되도록 할 수 있다
    
    ```Swift
    protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {
        // class-only protocol definition goes here
    }
    ```
    

  

# 프로토콜 혼합

- 동시에 여러개의 프로토콜을 준수하는 조건을 걸때 유용
    
    > `Named`, `Aged` 프로토콜을 동시에 준수하길 바랄 때
    
    ```Swift
    func wishHappyBirthday(to celebrator: Named & Aged) {
        print("Happy birthday, \(celebrator.name), you're \(celebrator.age)!")
    }
    ```
    
    - celebrator 파라미터에는 `Named`, `Aged`를 모두 채택한 `Person` 구조체도 올 수 있다