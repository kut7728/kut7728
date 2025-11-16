> [!important]
> 
> ### XCode16 → 페이지 타이틀 표현방식 선택
> 
> ```Swift
> .navigationTitle("프로필 편집")
> .navigationBarTitleDisplayMode(.inline)
> .navigationBarBackButtonHidden()
> ```

> [!important]
> 
> ### NavigationStack 과 NavigationLink
> 
> ```Swift
> import SwiftUI
> 
> struct ContentView: View {
>     @State var todoList: [Todo] = [
>         Todo(title: "Meeting friends"),
>         Todo(title: "Homework"),
>         Todo(title: "Working Out")
>     ]
>     
>     func addTodo() {
>         withAnimation {
>             let newTodo = Todo(title: "New Todo")
>             todoList.append(newTodo)
>         }
>     }
>     
>     func deleteTodo(indexSet: IndexSet) {
>         withAnimation {
>             for index in indexSet {
>                 todoList.remove(at: index)
>             }
>         }
>     }
>     
>     var body: some View {
>         NavigationStack {
>             List {
>                 ForEach(todoList) { todo in
>                     HStack{
>                         Image(systemName:
>                                 (todo.isCompleted ? "circle.fill" : "circle"))
>                         .foregroundStyle(Color.pink)
>                         .onTapGesture {
>                             todo.isCompleted.toggle()
>                         }
>                         
>                         NavigationLink {
>                             TodoDetailView(todo: todo)
>                             
>                             
>                         } label: {
>                             Text(todo.title)
>                                 .strikethrough(todo.isCompleted, color: .gray)
>                                 .foregroundStyle(todo.isCompleted ? Color.gray : Color.primary)
>                         }
>                         
>                         
>                     }
>                     .listRowSeparator(.hidden)
>                 }
>                 .onDelete(perform: deleteTodo)
>             }
>             .navigationTitle("ToDo 🏓")
>             .listStyle(.plain)
>             .toolbar {
>                 ToolbarItem {
>                     EditButton()
>                     
>                 }
>                 ToolbarItem {
>                     Button (action: addTodo, label: {
>                         Image(systemName: "plus")
>                     })
>                 }
>             }
>             
>         }
>     }
> }
> 
> \#Preview {
>     ContentView()
> }
> ```
> 
> ```Swift
> import SwiftUI
> 
> struct TodoDetailView: View {
>     @State var todo: Todo
>     
>     var body: some View {
>         VStack{
>             TextField("Todo title", text: $todo.title)
>                 .font(.title2)
>                 .padding(8)
>                 .overlay {
>                     RoundedRectangle(cornerRadius: 8)
>                         .stroke(Color.gray, lineWidth: 2)
>                 }
>             TextEditor(text: $todo.description)
>                 .font(.title2)
>                 .padding(8)
>                 .overlay {
>                     RoundedRectangle(cornerRadius: 8)
>                         .stroke(Color.gray, lineWidth: 2)
>                 }
>                 
>         }
>         .padding()
>         .navigationBarBackButtonHidden(true)
>         .navigationTitle("Edit Task 📝")
>         
>     }
> }
> 
> \#Preview {
>     TodoDetailView(todo: Todo(title: "2nd todo"))
> }
> ```

> [!important]
> 
> ### `.NavigationDestination` 을 통한 Pop to Root 구현
> 
>   
> 
>   
> 
> > 참고문헌
> 
> [https://www.hackingwithswift.com/forums/swiftui/navigationstack-pop-to-root/24439](https://www.hackingwithswift.com/forums/swiftui/navigationstack-pop-to-root/24439)