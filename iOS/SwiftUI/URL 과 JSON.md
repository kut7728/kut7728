### JSON 데이터 링크로부터 data 추출하기

```Swift
Task {
    let url = URL(string: "https://gvec03gvkf.execute-api.ap-northeast-2.amazonaws.com/")
    
    let (data, _) = try! await URLSession.shared.data(from: url!)
    
    let jsonString = String(data: data, encoding: .utf8)!
    print(jsonString)
}
```

- 하지만 여기까지 해도 데이터는 단순한 문자열에 지나지 않음 → 사용하기 편하도록 `Struct` 화 해야함

  

### JSONDecoder 로 데이터를 Struct 화 하기

```Swift
Task {
    let url = URL(string: "https://gvec03gvkf.execute-api.ap-northeast-2.amazonaws.com/")!
    
    let (data, _) = try! await URLSession.shared.data(from: url)
    
    let decoder = JSONDecoder()
    let dramaCollection = try! decoder.decode(DramaCollection.self, from: data)
    print(dramaCollection.bigBanner)
}

struct DramaCollection: Decodable {
    var bigBanner: String
    var dramas: [Drama]
    
    enum CodingKeys: String, CodingKey {
        case bigBanner = "BIG_BANNER"
        case dramas = "DRAMAS"
    }
}

struct Drama: Decodable {
    var categoryTitle: String
    var posters: [String]
    
    enum CodingKeys: String, CodingKey {
        case categoryTitle = "CATEGORY_TITLE"
        case posters = "POSTERS"
    }
}
```

- JSON의 정보를 가져올때는 `Decodable`, JSON으로 정보를 내보낼때는 `Encodable` → 둘다에 쓰이는 Struct는 `Codable`