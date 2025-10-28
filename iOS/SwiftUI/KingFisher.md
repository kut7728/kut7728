---
내용: 이미지 캐싱도 같이 해주는 asyncImage
유형: API
---
https://github.com/onevcat/Kingfisher

  

```Swift
else if let imageUrl = viewModel.user?.profileImageUrl{
    let url = URL(string: imageUrl)
    KFImage(url)
        .resizable()
        .frame(width: 75, height: 75)
        .clipShape(.circle)
        .padding(.bottom, 10)
}
```