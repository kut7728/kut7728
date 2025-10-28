---
내용: Auth, Firestore
유형: API
---
## Auth - 유저 인증

> [!important] **Firebase를 통한 유저 인증 솔루션**
> 
> - 홈페이지를 보면 다른 간편인증도 제공하는 듯 함
> - 인프런 강의에서 사용한 이메일 로그인의 경우 저장되는 값은 메일, 비밀번호, UID 뿐이므로 그 외 정보는 별도의 솔루션을 사용해야할 듯

  

> 유저 신규 추가

```Swift
func createUser(email: String, password: String, name: String, username: String) async {
    print("email : ", email)
    print("pw : ", password)
    print("name : ", name)
    print("username : ", username)
    
    do {
        let result = try await Auth.auth().createUser(withEmail: email, password: password)
        guard let userId = currentUserSession?.uid else { return }
        currentUserSession = result.user
        
        await uploadUserData(userID: userId, email: email, username: username, name: name)
        
    } catch {
        print("debug")
    }
}
```