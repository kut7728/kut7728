> [!warning] 요약
> 소셜 로그인 서비스는 OIDC 덕분에 가능한 것!

# OAuth VS OIDC
## > OAuth = 권한위임(인가)
- Authorization
- 요청한 클라이언트에게 데이터 제공 허용 여부를 결정하는 절차

## > OIDC = 로그인(인증)
- Authentication
- 이 사람이 누구인지 인증하는 것
- OAuth와 달리 ID Token([[JWT (JSON Web Token)]])을 통해 사용자의 정보를 제공받을 수 있음


# 소셜로그인의 흐름
- OAuth2 Authorization Code Flow → Access Token 발급 → OIDC Extension → ID Token 발급

