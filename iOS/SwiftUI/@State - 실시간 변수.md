---
내용: 실시간으로 뷰 업데이트하는 변수
유형: Wrapper
---
> [!important] `@State` 로 변수를 선언하고 `$’변수명’` 으로 저장한다!
> 
> 클래스의 객체인 변수라면 클래스에 `@Observable` 키워드 붙이기

  

### 개요

- 변수의 값이 변함에 따라 뷰를 자동으로 다시 그려줄 필요가 있는 경우 사용

  

### 일반 변수 예시

- 코드
    
    ```Swift
    struct ContentView: View {
        @State var nextWord: String = ""
        
        var body: some View {
            VStack {
                ...
                HStack {
                    TextField("단어를 입력하세요", text: $nextWord)
                        .padding()
                        .background(
                            RoundedRectangle(cornerRadius: 10)
                                .stroke(lineWidth: 2)
                        )
                    Text(nextWord)
                    ...
    ```
    

- 텍스트 필드 입력에 따라 값이 변하는 변수 `nextWord`는 Text 뷰에서 호출되고 있음
- 실시간 변수로 선언했기에 값이 달라질때마다 Text 뷰는 실시간으로 다시 그려짐
- 변수를 읽을 때는 그냥 변수 이름을 쓰면 되지만 저장 할때는 $이 붙어야 함

  

### 클래스 객체 변수 예시

- 코드
    
    ```Swift
    @Observable
    class Todo: Identifiable{
        let id: UUID
        var title: String
        var isCompleted: Bool
        var description: String
        
        init(title: String) {
            self.id = UUID()
            self.title = title
            self.isCompleted = false
            self.description = ""
        }
    }
    ```
    
    - 변수 호출시에 `@State` 붙이는 것은 똑같으나 클래스에도 `@observable` 키워드를 붙여줘야 함