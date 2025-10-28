---
내용: SecureField
유형: View
---
```Swift
TextField("단어를 입력하세요", text: $nextWord)
			.textInputAutocapitalization(.never)
      .padding()
      .background(
          RoundedRectangle(cornerRadius: 10)
              .stroke(lineWidth: 2)
      )
```

- 문자열 파라미터는 플레이스 홀더
- text 파라미터는 값을 저장할 변수
    - $ 기호의 경우 `실시간 변수` 페이지 참조

  

> [!important] TextField 대신 SecureField 로 가려진 비밀번호 입력 창 만들 수 있음