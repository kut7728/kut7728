## Guard 문

```Swift
guard condition1, condition2 else{
	statement
}
```

- 모든 condition이 true 면 guard문 이후로 진행, false면 else문 실행
- gaurd문 속 else문은 무조건 스코프가 중단되어야 함 (return 사용)
- if문과 달리 else문이 필수

> [!important] 조건이 늘어갈 수록 중첩이되는 if문과 달리 이어서 적기 때문에 가독성이 좋음

### guard 옵셔널 바인딩

```Swift
func printMessage(_ message: String?) {
	guard let letMessage = message else { return }
    print(letMessage)
}
printMessage(string)
```

`guard`를 사용하면 `if` 로 옵셔널 바인딩했을 때와 달리 { } 괄호 밖에서도 사용가능하다.

  

## Switch 문

```Swift
switch (valueExpression) {
	case pattern1:
		statements
		
	case pattern2, pattern3:
		statements
		
	default:
		statements
}
```

- `valueExpression` 과 `pattern` 이 일치한다면 해당 케이스 구문 실행
- `pattern` 에는 범위가 들어갈 수도 있고, 동일한 코드를 실행시킬 case끼리 결합도 가능
- 케이스 구문을 실행했다면 switch문을 중단한다.
- 만약 케이스 구문에 `fallthrough` 명령이 있다면 다음 케이스의 구문을 `pattern` 일치 여부와 상관없이 실행
- `default` 케이스의 구문에는 한줄 이상 작성 해야 함 (정 쓸게 없으면 `break` 사용)
- where 구문을 통해 pattern에 추가 조건도 붙일수 있음