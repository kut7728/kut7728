> [!important] 여러 항목들에 고유식별자를 제공해서 구분할 수 있도록 해줌

  

```Swift
class Todo: Identifiable{
    let id: UUID
    var title: String
    var iscomplete: Bool
    var description: String
    
    init(title: String) {
        self.id = UUID()
        self.title = title
        self.iscomplete = false
        self.description = ""
    }
}
```

- `Todo 클래스`의 객체들끼리 구분시켜주는 `UUID`
- `: Identifiable` 프로토콜을 따른다는 걸 알려줌

  

```Swift
ForEach(todoList, id: ...) { todo in
    HStack{
        Image(systemName: "circle")
            .foregroundStyle(Color.pink)
        NavigationLink {
            Text("next viewPage")
        } label: {
            Text(todo.title)
        }
    }
}
```

- todoList의 원소들은 `UUID`가 있고 `: Identifiable`을 통해 UUID 프로토콜을 따른다는 것을 명시했기 때문에 `id 파라미터`를 굳이 넣어줄 필요 없다!