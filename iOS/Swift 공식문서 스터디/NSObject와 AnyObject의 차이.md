  

# **NSObject란?**

- NSObject는 Objective-C와 Swift에서 사용되는 대부분의 **클래스 계층 구조의 루트(최상위) 클래스**입니다.
- Foundation 프레임워크의 핵심이자, Cocoa 및 Cocoa Touch의 거의 모든 클래스가 NSObject를 상속받습니다.
    - NSObject는 객체 초기화, 메모리 관리, 객체 비교, 복사 등 기본적인 기능을 제공합니다
    - Objective-C의 런타임 시스템과 상호작용할 수 있는 기본 인터페이스를 제공합니다.

> [!important] 대부분의 UIKit 핵심 클래스들은 이미 NSObject를 상속 받음
> 
> - 덕분에 KVO, 런타임 시스템의 기능들을 사용 가능
> 
>   
> 
> SwiftUI는 View프로토콜이라 NSObject를 상속받지 않음
> 
> - KVO 사용하고 싶으면 NSObject 상속받고 @objc 사용해야함
> - 델리게이트 패턴을 사용하고자 할때도 상속 받아야 함

[https://green1229.tistory.com/534](https://green1229.tistory.com/534)

  

# **AnyObject란?**

- Swift의 모든 클래스는 AnyObject 프로토콜을 암시적으로 준수합니다
- AnyObject는 Swift에서 **"모든 클래스 타입의 인스턴스"**를 나타내는 **프로토콜**입니다
    - 즉, AnyObject는 클래스(Reference Type)로 만들어진 객체만을 담을 수 있습니다.
    - 구조체(Struct), 열거형(Enum) 등 값 타입(Value Type)은 AnyObject에 담을 수 없습니다
- AnyObject는 Objective-C의 id 타입과 유사하며, Objective-C와의 상호 운용성을 위해 자주 사용됩니다

  

  

> [!important]
> 
> # Any는요?
> 
> - 함수타입을 포함하여 모든 타입의 인스턴스를 나타내는 타입

[https://zeddios.tistory.com/213](https://zeddios.tistory.com/213)