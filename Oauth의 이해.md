# Oauth
- 사용자가 제 3자 서비스를 사용할때 직접 비밀번호를 입력하지않고 신뢰할수 있는 외부 어플리케이션을 통해 로그인하는 방식
- Google, Apple, Kakao의 소셜 로그인이 Oauth 인증 흐름을 기반으로 함
- 사용자의 비밀번호를 노출하지 않고 토큰을 통해 안전하게 인증 가능
- 필요한 권한만 제한적으로 제공 가능(Scope)

# 핵심개념
- 클라이언트 : 로그인이 이루어지는 환경 (앱, 웹, 서버등)
- Resource Owner : 사용자
- Authorization Server : Google, Apple과 같은 인증 서버
- Redirect URI^[[[URL과 URI]]]  : 인증 후 코드를 돌려주는 URL
- Authorization Code : Access Token을 받을 때 사용하는 “일회용 코드”
- Access Token : API 접근에 쓰이는 실제 권한 토큰
- Refresh Token : Access Token이 만료되면 새로 발급받는 토큰
- Scope : 인증 서버측 정보중에서 사용하고자하는 사용자의 정보

# Oauth 인증 흐름
1. 유저 → 구글 로그인 페이지로 이동
2. 로그인 성공 → Redirect URL로 Authorization Code 전달
3. 앱/서버 → Authorization Code로 Access Token 요청
4. Access Token + Refresh Token 발급
5. Access Token으로 사용자 정보 가져오기

# 모바일 앱의 Oauth 인증 흐름

> [!warning] PKCE
> PKCE의 핵심 아이디어
> 	•	앱이 임시 비밀번호 (코드 챌린지) 를 만들어 서버에 먼저 전달
> 	•	인증 후 받은 Authorization Code 와 이 챌린지를 함께 보내야 Token 발급됨
> 	•	이렇게 하면 토큰 탈취 공격을 막을 수 있음

1. Flutter 앱에서 code_verifier 생성
2. code_challenge = SHA256(code_verifier)
3. 로그인 요청 시 code_challenge를 Authorization Server로 보냄
4. 인증 성공 → code 전달
5. Token 요청 시 code_verifier로 검증
6. Access Token 발급

# [[OIDC (OpenID Connect)]]
- Google, Apple 로그인 같은 소셜로그인들은 Oauth 2.0 위에 OIDC가 올라간 구조
- OIDC는 OAuth2의 확장중 하나로써 인증(Authentication)에 대한 프로토콜
- 각 인증 서비스제공자들에게서 받는 ID Token속의 사용자 정보(이름, 메일주소)등을 파싱해서 사용 가능