---
내용: 그래디언트 주기
유형: View
---
### 기본 LinearGradient 뷰

```Swift
LinearGradient(colors: [Color.blue, Color.red], startPoint: .top, endPoint: .bottom)
```

- 색을 추가해서 더 다양한 그래디언트 가능

  

### 세부 LinearGradient 뷰

```Swift
LinearGradient(stops:[
            Gradient.Stop(color: .red, location: 0.2),
            Gradient.Stop(color: .blue, location: 0.8),
        ], startPoint: .topLeading, endPoint: .bottomTrailing)
```