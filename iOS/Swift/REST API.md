## API

1. 서버가 제공하는 데이터나 기능을 프로그램이 사용할 수 있도록 해주는 인터페이스
2. 서버 시스템의 내부 프로세스는 숨긴채 유용한 기능과 정보 제공을 목적으로 함

  

## HTTP API

- HTTP 통신 규칙으로 소통하는 API
    
    `HTTP 대신 다른 프로토콜을 사용하는 API도 존재`
    

  

## REST API

HTTP의 장점을 최대한 끌어내기 위한 네트워크의 자원을 정의하고 처리하는 방법을 만들었는데

그것이 REST 네트워크 아키텍처 스타일

  

> 즉 REST API = REST 원칙을 준수해 만든 HTTP API

  

> [!important]
> 
> ### REST 의 4가지 가이드 원칙
> 
> 1. 자원의 식별
> 2. 메세지를 통한 리소스 조작
> 3. 자기서술적 메세지
> 4. 어플리케이션의 상태에 대한 엔진으로서 하이퍼미디어
>     
>     → 이 조건을 완벽하게 지키면서 개발하는 것을 RESTful API 라고 함
>     

> [!important]
> 
> ### REST의 특징
> 
> 1. Server-Client(서버-클라이언트 구조)
> 2. Stateless(무상태)
> 3. Cacheable(캐시 처리 가능)
> 4. Layered System(계층화)
> 5. Uniform Interface(인터페이스 일관성)

> [!important]
> 
> ### URI - 자원(데이터)을 정의할때 4가지 방식으로 표현
> 
> - document → 1개의 객체
> - collection → document들의 집합
> - store
> - controller
> 
> `명사형 단어만을 사용해서 자원을 표현`
> 
> `행위는 HTTP Method 로 따로 표현`
> 
> `소문자만 사용`
> 
> `밑줄 대신 하이픈만 사용`

  

> [!important]
> 
> ### URI vs URL
> 
> > URI - Uniform Resource Identifier / 통합 자원 식별자
> 
> - 인터넷 상의 자원 자체를 식별하는 고유한 문자열 시퀀스
> 
>   
> 
> > URL - Uniform Resource Locator
> 
> - 인터넷 상의 자원의 위치를 나타내기 위한 규약
>     
>     → 즉, 식별자 + 위치
>     
> - https, http, ftp 등의 프로토콜을 포함하고 있음
> 
>   
> 
> ![[241007144300hI8lp.jpg.jpg]]

  

> [!important]
> 
> ### 자원에 대한 행위의 표현
> 
> `HTTP Method(GET, POST, PUT, DELETE)로 표현`
> 
> |Method|정의|CRUD|
> |---|---|---|
> |GET|리소스를 조회하고 정보를 가져옵니다.|READ|
> |POST|리소스를 생성합니다.|CREATE|
> |PUT|해당 리소스를 수정합니다.|CREATE or UPDATE|
> |PATCH|해당 리소스를 수정합니다.(일부만 수정)|UPDATE|
> |DELETE|해당 리소스를 삭제합니다.|DELETE|

  

```Python
http://restapi.example.com/sports/soccer/players/13
```

- sports, players 라는 collection
- soccer, 13 이라는 document 로 이루어진 URI

  

  

> 참고

[https://bentist.tistory.com/37](https://bentist.tistory.com/37)

[https://www.elancer.co.kr/blog/detail/74](https://www.elancer.co.kr/blog/detail/74)

[https://velog.io/@yewo2nn16/Spring-%EC%98%88%EC%A0%9C%EC%99%80-%ED%95%A8%EA%BB%98-REST-API-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90](https://velog.io/@yewo2nn16/Spring-%EC%98%88%EC%A0%9C%EC%99%80-%ED%95%A8%EA%BB%98-REST-API-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)