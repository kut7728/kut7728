```Swift
@State var showAlert = false

...
Button {
    showAlert = true
} label: {
    Text("약속 취소")
}
.alert("끝말잇기가 이어지는 단어를 입력해주세요", isPresented: $showAlert) {
    Button("확인", role: .cancel) {
        showAlert = false
    }
}
```

- `isPresented 파라미터` : 여기 입력되는 값에 따라 알림창 출력 여부 결정
    - 버튼 액션에 따라 값이 변하고 실시간으로 뷰를 재실행 해야하기 때문에 변수는 `$State` , 호출시에도 `$` 를 붙여야 함
- Button 뷰 속 `role 파라미터`
    - `.cancel` : 사진과 같이 알림창을 닫는 버튼 하나만 존재하는 뷰
        
        ![[CleanShot_2024-11-29_at_00.22.312x.png]]
        
    - `.destructive` : 빨간색 취소와 파란색 확인 버튼 두개가 뜨는 뷰

  

> [!important]
> 
> ### 커스텀 얼럿 만들기
> 
> [https://iosangbong.tistory.com/6](https://iosangbong.tistory.com/6)
> 
> [https://reusablecode.tistory.com/18](https://reusablecode.tistory.com/18)