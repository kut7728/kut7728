---
내용: 취소선, 폰트 크기
유형: View
---
### 취소선 modifier

```Swift
Text(todo.title)
      .strikethrough(todo.isCompleted, color: .gray)
```

- [1] 어떤 상황에서 취소선 그을지
- [2] 취소선 색깔

  

### 폰트 크기

```Swift
Text("폰트 크기 조절")
		.font(.system(size: 32))
```