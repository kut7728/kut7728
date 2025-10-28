```Swift
for i in 1...5 {
	print("안녕하세요")
}   
// 1 부터 5까지 다섯번 반복


for i in 1..<5 {
	print("안녕하세요")
}
// 1 부터 4까지 네번 반복
```

  

### 문자열 포맷 (String Interpolation)

```Swift
for i in 1...9 {
	print("2 * \(i) = \(2*i)")
}
```

  

### .forEach

```Swift
let things = ["ps5", "pc", "switch"]

things.forEach { console in
	print(console)
}

things.forEach {
	print($0)
}
```