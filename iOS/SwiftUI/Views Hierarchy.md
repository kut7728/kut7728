> [!important] 여러개의 View를 감싸서 같이 출력해줌, Stack 없이는 하나의 View만 출력됨

### Vstack

: 자식 view 들을 세로로 쌓음

```Swift
VStack {
    Text("Learning to code!")
        .font(Font.custom("Helvetica", size: 16))
    Text("I'm happy")
}
.font(.title)
```

- Vstack 에 직접 영향을 주는 Modifier
    - `padding()`
    - `border()`
- Vstack 의 자식들 전부에게 영향을 주는 Modifier
    - `font()`
    - `foregroundColor()`
    - 만약 자식 View 에 붙은 Modifier가 있다면 그게 우선권
- 자식 View 의 정렬과 간격은 Modifier 를 붙이는 대신에 선언할 때 설정도 가능
    
    - 정렬의 기본값은 중앙정렬
    - `alignment: .leading` : 좌측정렬
    
    ```Swift
    VStack(alignment: .leading, spacing: 10) {
        Text("Learning to code!")
        Text("I'm happy")
    }
    ```
    
      
    

### Hstack

: 자식 View 들을 가로로 이어 보여줌

```Swift
HStack(alignment: .top, spacing: 10) {
    Text("Learning to code!")
        .foregroundColor(.white)
        .font(Font.custom("Helvetica", size: 20))
        .padding(10)
        .background(Color.blue)
    Text("I'm happy")
        .font(Font.custom("Helvetica", size: 12))
        .padding(20)
        .background(Color.gray)
}
```

  

### Zstack

: 자식 View 들을 쌓아서 보여줌, 뒤에 쓰인 View 가 위로 감

![[zstack_bottom.webp]]

```Swift
ZStack(alignment: Alignment(horizontal: .leading, vertical: .bottom)) {
    VStack {}
        .frame(width: 200, height: 200)
        .background(Color.blue)
    VStack {}
        .frame(width: 100, height: 100)
        .background(Color.yellow)
}
.font(.title)
.foregroundColor(.green)
.border(Color.black)
```