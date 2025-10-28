#NextJS 
# 개요
- React에서 **params**는 Next.js App Router의 동적 라우팅에서 사용되는 URL 파라미터입니다.

``` ts
// 폴더 구조: /dashboard/[teamId]/settings
// URL: /dashboard/123/settings

// page.tsx
type Props = {
  params: {
    teamId: string;  // "123"
  };
};

export default function Page({ params }: Props) {
  console.log(params.teamId); // "123"
  return <PageView teamId={Number(params.teamId)} />;
}
```

# 특징
## 1. 동적 세그먼트

- `[teamId]` → 폴더명의 대괄호가 동적 파라미터가 됩니다
- URL의 해당 위치 값이 `params.teamId`로 전달됩니다

## 2. 타입은 항상 string

- URL 파라미터는 기본적으로 문자열입니다
- 숫자로 사용하려면 `Number(params.teamId)` 변환 필요

## 3. 중첩 가능

``` ts
// /dashboard/[teamId]/chat/[chatId]
type Props = {
  params: {
    teamId: string;
    chatId: string;
  };
};
```

## 4. Server Component에서만 사용

- `page.tsx`, `layout.tsx`, `generateMetadata` 등에서 사용
- Client Component에서는 직접 접근 불가
 
``` ts
// Client Component에서 직접 접근 불가
"use client";

export default function PageView({ params }) {
  // params를 직접 받을 수 없음
}

// Props로 전달받아 사용
"use client";

type Props = {
  teamId: number;  // 이미 변환된 값
};

export function PageView({ teamId }: Props) {
  // teamId 사용
}    
```
