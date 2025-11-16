```Swift
struct ContentView: View {
    
    @State private var wakeUp = Date()
    
    var body: some View {
        DatePicker("날짜를 선택하세요", selection: $wakeUp)
            .labelsHidden()
            .datePickerStyle(.automatic)
            .environment(\.locale, Locale(identifier: String(Locale.preferredLanguages[0])))    
      }
}
```

  

[https://green1229.tistory.com/404](https://green1229.tistory.com/404)