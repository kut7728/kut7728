#렌더링 #NextJS

# 개요

Header, Footer, Sidebar 등 공통적으로 사용되는 요소들을 컴포넌트 복사대신 재활용 할 수 있게 해주는 Next.js의 시스템

# Layout.tsx의 역할

Next.js는 `app` 디렉토리 내부에서 `layout.tsx` 파일을 감지하여, 해당 폴더와 그 하위 경로의 페이지 컴포넌트들을 감싸는 기본 UI 틀로 사용

예를 들어 프로젝트 루트(`app/layout.tsx`)에 정의하면 애플리케이션 전 영역의 공용 구조(예: Header, Footer 등)를 담당한다. 또 `/admin/layout.tsx`처럼 하위 디렉토리에 정의하면, 특정 경로(`/admin` 이하)에만 다른 레이아웃이 적용된다.

# default export 함수

Next.js는 각 라우트의 `layout.tsx`를 자동으로 인식하고 렌더링 트리 구조에 포함시키기 위해 **기본 내보내기(default export)** 를 요구한다.  
레이아웃 함수를 기본 내보내기로 선언하지 않으면 Next.js에서 이를 유효한 레이아웃 컴포넌트로 인식하지 못한다.

``` ts
import type { Metadata } from 'next'

export const metadata: Metadata = {
  title: 'My App',
  description: 'Example layout.tsx'
}

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="ko">
      <body>
        <header>공통 헤더</header>
        <main>{children}</main>
        <footer>공통 푸터</footer>
      </body>
    </html>
  )
}

```

# 중첩렌더링

Next.js는 더 깊은 폴더에 또 다른 `layout.tsx`가 있으면 이를 **중첩하여 렌더링**한다.

``` ts
<RootLayout>
  <AdminLayout>
    <Page />
  </AdminLayout>
</RootLayout>

```


# 요약

`layout.tsx`의 `default export`는 Next.js에서 페이지 구조를 구성하는 최상위 JSX 래퍼를 지정하는 필수 규칙이며, 중첩·상속을 통해 계층형 UI를 효율적으로 관리하는 데 사용된다.