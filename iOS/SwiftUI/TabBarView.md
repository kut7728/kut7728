---
유형: View
---
```Swift
var body: some View {
    @State var tabIndex = 0
    
    TabView(selection: $tabIndex) {
        Text("Feed")
            .tabItem { Image(systemName: "house") }
            .tag(0)
        Text("Search")
            .tabItem { Image(systemName: "magnifyingglass") }
            .tag(1)
        NewPostView()
            .tabItem { Image(systemName: "plus.square") }
            .tag(2)
        Text("Reels")
            .tabItem { Image(systemName: "movieclapper") }
            .tag(3)
        Text("Profile")
            .tabItem { Image(systemName: "person.circle") }
            .tag(4)
    }
    .tint(Color.black)
}
```