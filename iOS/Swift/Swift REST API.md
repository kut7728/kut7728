---
설명: URLSession, URLRequest, Alarmofire
---
## URLSession

`애플 기본 서버 통신 API`

```Swift
func loadData() async {
		guard let url = URL(string: "http://something.com") else {
				print("Invalid URL")
				return
		}
		
		do {
				let (data, _) = try await URLSession.shared.data(from: url)
				
				if let decodedResponse = try? JSONDecoder().decode(Response.self, from: data) {
						results = decodedResponse.results
				}
						
		} catch {
				print("Invalid data")
		}

}
```

  

## Alarmofire 라이브러리

### GET 메소드 호출

```Swift
AF.request("http://localhost:5000/test/get").responseJSON() { response in
  switch response.result {
  case .success:
    if let data = try! response.result.get() as? [String: Any] {
      print(data)
    }
  case .failure(let error):
    print("Error: \(error)")
    return
  }
}
```

  

### POST 메소드 호출

```Swift
AF.request("http://localhost:5000/test/post", method: .post, parameters: ["key": "hello!"], encoding: URLEncoding.httpBody).responseJSON() { response in
  switch response.result {
  case .success:
    if let data = try! response.result.get() as? [String: Any] {
      print(data)
    }
  case .failure(let error):
    print("Error: \(error)")
    return
  }
}
```

  

  

  

[https://jazz-the-it.tistory.com/19](https://jazz-the-it.tistory.com/19)

> [!info] Sending and receiving Codable data with URLSession and SwiftUI – Cupcake Corner SwiftUI Tutorial 1/9  
> Download the completed project here: https://github.  
> [https://www.youtube.com/watch?v=U_yWXH141DY](https://www.youtube.com/watch?v=U_yWXH141DY)