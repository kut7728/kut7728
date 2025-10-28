#Hook

# 개요
- React의 **메모이제이션(memoization)** 훅이에요.
- 계산 결과를 **캐싱**해서, 의존 값이 바뀌지 않는 한 다시 계산하지 않도록 해줍니다.

# 특징
``` ts
const memoizedValue = useMemo(() => {
  // 계산이 오래 걸리는 코드
  return result;
}, [dependency]);
```
- 첫 번째 인자로 전달된 함수를 실행해서 나온 결과값을 기억함
- 두 번째 인자인 **의존성 배열(dependency array)** 안의 값이 변하지 않는 한 그 결과를 **다시 계산하지 않고 캐시된 값**을 그대로 반환합니다.

> [!info] 주요 사용처
> sort(), find() 처럼 무거운 계산의 결과값을 캐싱하는데 자주 사용됨



# 예시
``` ts hl:3
const currentTeam = useMemo(
  () => teams.find((value) => value.id === Number(currentTeamId)),
  [currentTeamId, teams],
);
```
- teams의 요소들 중 id가 currentTeamId와 일치하는 항목 반환
- 3번줄의 배열 속 값이 바뀔 때만 함수를 다시 실행