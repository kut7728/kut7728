```Swift
ScrollView (.horizontal) {
    HStack {
        Spacer()
        ForEach(0..<3) { _ in
            AppointPickedFriendCellView()
        }
        Spacer()
    }
    .frame(width: .infinity)
    .border(.black)
}
.defaultScrollAnchor(.center)
```

![[CleanShot_2025-01-17_at_18.25.552x.png]]

  

![[1bde285a-824b-4fae-a603-052ba10ae1f6.png]]