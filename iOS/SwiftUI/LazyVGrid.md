---
내용: 순차 읽어오기가 되는 그리드 뷰
유형: View
---
```Swift
let columns: [GridItem] = [
    GridItem(.flexible(), spacing: 2),
    GridItem(.flexible(), spacing: 2),
    GridItem(.flexible(), spacing: 2)
]

LazyVGrid(columns: columns, spacing: 2) {
    ForEach(0..<10) { _ in
        Image("image_dog")
            .resizable()
            .scaledToFit()
        Image("image_dragon")
            .resizable()
            .scaledToFit()
        Image("image_lion")
            .resizable()
            .scaledToFit()
        Image("image_penguin")
            .resizable()
            .scaledToFit()
        Image("profile_cat")
            .resizable()
            .scaledToFit()
    }
    
}
```

![[CleanShot_2025-01-13_at_01.35.122x.png]]