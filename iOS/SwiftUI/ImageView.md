```Swift
Image("dogProfile")
	  .resizable()
	  .frame(width: 120, height: 120)
	  .clipShape(Circle())
	  .overlay(
			  Circle()
					  .stroke(Color.teal, lineWidth: 3))
```

- `Image 뷰`는 원래 이미지 전체 크기를 전부 출력 → `.resizable` 로 편집허용
- `.frame` 으로 크기 조정
- `.clipShape` 으로 형태 조정
- `.overlay` : 이미지 위에 `Circle()` 얹기 (like ZStack) → `.stroke` : Circle의 테두리만 얹기

  

---

  

### `.aspectRatio`

```Swift
Image("image_lion")
    .resizable()
    .aspectRatio(1, contentMode: .fit)
    .frame(maxWidth: .infinity)
    .clipped()
```

- `.aspectRatio()` 의 `.fit` 은 `.scaledToFit()` 과 동일
- `.aspectRatio()` 의 `.fill` 은 `.scaledToFill()` 과 동일