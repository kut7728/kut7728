> [!important]
> 
> ### Model - View - ViewModel
> 
> MVC 패턴의 Controller 의 역할을 분산시킨 디자인 패턴  
> Model 의 변경점을 Binding을 통해서 View 에 반영  
> 
> 💡 UIKit 의 경우 Binding 이 기본이 아니어서 MVVM 어려웠으나 `Combine` 을 통해 가능!

![[e84be834-b046-46ce-815d-419c9fc0318c.png]]

  

### 실습 코드

```Swift
import SwiftUI

// << MODEL >>
struct NumberModel {
    var number: Int
}

// << VIEW MODEL >>
@Observable
class ContentViewModel {
    var model = NumberModel(number: 0)
    
    func plusLogic() {
        if model.number % 2 == 0 { //2로 나누어서 나머지가 0이면 = 짝수이면
            model.number += 1
        } else { //홀수이면
            model.number *= 2
        }
    }
}

// << MODEL >>
struct ContentView: View {
    @State var viewModel = ContentViewModel()
 
    var body: some View {
        VStack {
            Text("\(viewModel.model.number)")
            Button(action: {
                viewModel.plusLogic()
            }, label: {
                Text("증가")
            })
        }
        .padding()
    }
}

\#Preview {
    ContentView()
}
```