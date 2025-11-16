> [!important] 같은 기능을 줄여서 적을 수 있다!
> 
> `.compactMap` 은 nil을 뛰어 넘어서 적용 가능

```Swift
var posts: [Post] = []
for document in documents {
    let post = try document.data(as: Post.self)
    posts.append(post)
}
self.posts = posts
```

```Swift
self.posts = try documents.map({ document in
    return try document.data(as: Post.self)
})
```