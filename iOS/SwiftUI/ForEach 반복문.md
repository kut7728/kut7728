---
내용: 뷰를 반복하고 싶을 때
유형: View
---
> [!important] 스크롤되는 Cell 뷰를 ForEach로 호출하면 모든 내용을 한번에 긁어오기 때문에 성능이슈 발생
> 
> 대신에 `List 뷰` / `스크롤 뷰` + `LazyVStack` 활용할 것

  

```Swift
ForEach (1..<6) {number in
	Text("Hello")
}
```

- ForEach 에서는 `(1...5)` 사용 불가
    - 오직 부등호를 넣어서만 사용 가능

  

### id

```Swift
ForEach(words.reversed(), id: \.self) { word in
    Text(word)
        .font(.title2)
}
```

- id 파라미터는 배열 속 항목들을 구분하는 방법을 제시해줌
- `\.self` 는 항목의 값 그 자체로 구분을 하라는 의미
    - 이런 방식은 배열속에 중복되는 항목이 있을 때 에러를 만들게 됨
- `UUID` 페이지 참조