# 종류
- var - 더이상 쓰지 않음
- let
- const

let과 var은 변수, 비운채로 선언가능
const는 상수, 무조건 초기화해야함

# Hoisting
- 모든 변수 선언문이 코드 최상단에서 선언되듯이 동작함
- 변수 초기화 전에 출력을 해도 undefined로 출력이 되버림;;
- var, let, const 전부 동일하게 Hoisting 됨
> [!warning] var가 안쓰이는 이유
> Hoisting은 var, let, const 전부 동일하게 적용되지만.
> let과 const는 사용자 초기화 전에 접근을 막아줌, 이런 연유로 var는 안쓰이는거임

