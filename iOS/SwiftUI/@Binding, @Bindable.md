---
내용: 하위 스코프에서 실시간 변수 이어쓰기
유형: Wrapper
---
> [!important] @State 변수를 다른 구역에서도 이어서 쓰기위한 랩퍼 → @Binding
> 
> @Observable 변수(Class에 사용)를 다른 구역에서도 이어서 쓰기 위한 랩퍼 → @Bindable

```Swift
struct ContentView: View {
	@state var text: String = ""

	var body: some View {
		VStack {
			Text(text)
				.border(.blue, width: 1)
				
			TextField("글자를 입력해주세요", text:$text)
			Button ("하트추가") {
				text = text + "❤️"
			}
			
			Divider()
			MyView(text: $text)
		}
	}
}
```

```Swift
import SwiftUI

struct MyView: View {
	@Binding var text: String

	var body: some View {
		Text("My View")
		Text(text)
		Button ("하트추가") {
			text = text + "❤️"
		}
	}
}
```