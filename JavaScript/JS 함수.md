# 기본 형태
``` js
function cal(x, y) {
	console.log((x * y).toString);
	return x * y;
}

const result = cal(2, 4);  // 8
```
- 파라미터의 기본값 제공
	- `function cal(x, y = 10){}`


# 화살표 함수
``` js
let multiply2 = (x, y) => {
	return x * y;
}

let multiply3 = (x, y) => x * y;
```
- 파라미터가 하나라면 파라미터 괄호도 생략 가능

# 즉시 실행 함수
``` js
(function(x, y){
	console.log(x * y);
})(4, 5)  // 20
```
- 이름 없이도 선언가능, 대신 바로 호출되도록 해야 함

# 활용
``` js
const multiplyAll = function (...arguments) {
	return Object.values(arguments).reduce((a,b) => a * b, 1);
}
```
- 파라미터를 무한히 받음
- 받은 어규먼트들을 하나씩 곱해서 반환