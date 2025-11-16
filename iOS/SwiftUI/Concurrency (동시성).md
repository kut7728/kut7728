> [!important] url을 통해 데이터를 불러오는 등의 작업은 로딩에 시간을 잡아먹어 편의성에 지장을 줄 수 있다.
> 
> 오래 걸리는 작업은 xcode에서 `Option키`를 누르고 확인할때 async 표기가 되어 있다.

  

### Async, Await

```Swift
Task {
	print("시작")
	await Task.sleep(2_000_000_000)
	print("끝")
}
```

- 실습
    
    ```Swift
    func convertImage(item: Photospickeritem?) async {
    		guard let item = item else { return }
    		guard let data = try? await item.loadTransferable(type: Data.self) else { return }
    		guard let uiimage = UIImage(data: data) else { return }
    		self.postimage = Image(uilmage: uilmage)
    }
    
    ...
    
    Task {
    		await convertImage(item: image)
    }
    ```
    

  

> [!important]
> 
> ### 이중 작업
> 
> ```Swift
> extension AuthManager {
>     func follow(userId: String) async {
>         guard let currentUserId = currentUser?.id else { return }
>         
>         do {
>             async let _ = try await Firestore.firestore()
>                 .collection("following")
>                 .document(currentUserId)
>                 .collection("user-following")
>                 .document(userId)
>                 .setData([:])
>             
>             async let _ = try await Firestore.firestore()
>                 .collection("follower")
>                 .document(userId)
>                 .collection("user-follower")
>                 .document(currentUserId)
>                 .setData([:])
>                 
>         } catch {
>             print("DEBUG: Error following user: \(error.localizedDescription)")
>         }
>     }
> }
> ```

  

### Task

> [!important] 메인 쓰레드가 아닌 다른 쓰레드로 일을 넘기는 함수

```Swift
print("hello")
Task{
		var number = 0
		for i in 0...200000 {
				number += i
		}
		print("for \(number) times")
}
print("world")
```

```Swift
hello
world
for 20100 times
```