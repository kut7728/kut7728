---
내용: 리스트 뷰
유형: View
---
> [!important] 아이폰 기본 리스트 뷰 스타일

  

### 섹션

기본 리스트 뷰에는 아이폰 설정앱 처럼 구획이 나눠져 있음

![[CleanShot_2024-11-28_at_23.19.292x.png]]

```Swift
List {
    Section(header: Text("단어")) {
        ForEach(words, id: \.self) { word in
            Text(word)
                .font(.title2)
        }
    }
    Section(header: Text("단어2")) {
        ForEach(words, id: \.self) { word in
            Text(word)
                .font(.title2)
        }
    }
}
// .listStyle(.plain)
```

- 섹션을 해제하고 싶다면 `.listStyle(.plain)` 추가
- 리스트 행 구분선 없애려면 각 행 밑에 `.listRowSeperator(.hidden)` 추가

  

### `.toolbar` 메소드

![[CleanShot_2024-11-29_at_13.50.402x.png]]

```Swift
.toolbar {
    ToolbarItem {
        EditButton()
        
    }
    ToolbarItem {
        Button (action: {
            print("pressed")
        }, label: {
            Image(systemName: "plus")
        })
    }
}
```