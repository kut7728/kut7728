- 목차
    - [[#View]]
    - [[#View Modifiers]]
        - [[#Color]]
        - [[#Font]]
        - [[#Multi line text alignment]]
        - [[#Padding]]
        - [[#Background]]
    - [[#Color]]
    - [[#Button]]
    - [[#Spacer]]

## View

: IOS의 화면을 채우는 요소

```Swift
struct ContentView: View {
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundStyle(.tint)
            Text("Hello, world!")
        }
        .padding()
    }
}
```

  

## View Modifiers

: View에 속성을 부여하는 방법

```Swift
Text("I'm happy!")
   .border(Color.black, width: 1)
   .padding()
```

> [!important] **Modifiers 는 적힌 순서대로 적용됨**
> 
>   
> 여백을 주는 padding 보다 경계선을 그리는 border가 먼저 적용되기 때문에  
> padding 을 적었지만 여백없이 텍스트에 밀착한 경계선이 출력됨

### Color

`.foregroundColor(.blue)` - 구형 뷰, 곧 사라질 예정이므로 지양하자

`.foregroundStyle(.blue)`

### Font

`.font(.title)`

`.font(Font.custom("Helvetica", size: 24))`

`.bold()`

### Multi line text alignment

`.multilineTextAlignment(.center)`

### Padding

: 여백 넣기

`.padding(EdgeInsets(top: 3, leading: 5, bottom: 10, trailing: 20))`

`.padding(.top, 10)`

### Background

`.background(.black)`

> [!important]
> 
> - `[Color.black](http://Color.black)` 은 컬러값이 아닌 뷰의 일종이다
> - `background modifier`는 배경으로 다른 뷰를 넣어주는 역할이므로 색이 아닌 다른 뷰도 배경으로 넣을 수 있다 (ex. circle 뷰, rectangle 뷰)
> 
>   

  

  

  

## Color

![[Color.webp]]

```Swift
ZStack {
    Color.blue
    Text("I'm blue!")
        .font(.title)
        .foregroundColor(.white)
}
```

- color 는 view이기 때문에 다른 view처럼 단독적으로 사용 가능
    
    → 이런 경우 배경처럼 색깔이 밑에 깔리게 됨
    
- 상단과 하단의 하얀부분은 Safe area 라고 부르고 시스템 요소들이 들어감
    - `.ignoresSafeArea()` 통해서 무시 가능

## Button

```Swift
VStack {
    Text("Welcome to Code History!")
        .font(.title)
        .padding()
    Button(action: {
        print("Clicked")
    }, label: {
        Text("Click me")
    })
    .padding()
    .background(Color.blue)
    .foregroundColor(.white)
}
```

  

## Spacer

- 공간을 차지하기 위한 View
- 어떤 컨테이너에 넣냐에 따라 가로와 세로중에 차지할 위치 달라짐

```Swift
HStack {
    Spacer()
        .frame(width: 100)
    Text("I'm blue!")
        .font(.title)
        .foregroundColor(.blue)
}
```

- Hstack에 들어간 Spacer 는 가로로 너비 100px 만큼 차지함
- `.frame(width: 100)` 없다면 가로로 전체를 잡아먹고 text를 오른쪽 끝까지 밀어버림