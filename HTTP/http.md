# HTTP(HyperText Transfer Protocol)

문서간의 링크를 통해 정보를 주고 받는 기술  
지금은 HTTP 메세지에 모든 것을 전송  
- HTML, TEXT, IMAGE, 음성, 영상, 파일, JSON, XML, 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

# HTTP 역사

# HTTP 기반 프로토콜
TCP: HTTP/1.1, HTTP/2  
UDP: HTTP/3 점점 증가

# HTTP 특징
### 01. 클라이언트 서버 구조
- request, response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답

### 02. 무상태 프로토콜(Stateless)
- 서버가 클라이언트의 상태를 보존X

### 03. 비연결성(conectionless)
- 최소한의 자원 사용
- 한계: 3 way handshake 시간 추가
- 지금은 HTTP 지속 연결(Persistent Connections)으로 문제 해결

### 04. HTTP 메세지
HTTP 메세지 구조
1. start-line
   - 요청: [http 메서드]  + [요청대상] + [HTTP 버전]
   - 응답: [HTTP 버전] + [상태코드]
2. header
	- field-name ":" OWS(띄어쓰기허용) field-value OWS
	- 대소문자 구분 X
	- 메세지 바디의 내용, 메세지 바디의 크기 등등 바디에 대한 모든 메타데이터
3. empty line
4. message body
  - 실제 전송할 데이터
  - HTML, 이미지, 영상 등

# HTTP 메서드 종류
### 01. GET
- 리소스 조회
- 전달하고 싶은 데이터는 query string 을 통해서 전달
- 메세지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

### 02. POST
- 요청 데이터 처리
- 메세지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 신규 리소스 등록 및 프로세스 처리

### 03. PUT
- 리소스를 있으면 대체
- 리소스가 없으면 생성
- 덮어쓰기
- 클라이언트가 리소스의 위치를 알고 URI 지정

### 04. PATCH
- 리소스를 부분 변경

### 05. DELETE
- 리소스를 삭제

# HTTP 메서드의 속성
### 안전 GET, HEAD
- 호출해도 리소스를 변경하지 않는다. 

### 멱등(indempotent) GET, PUT, DELETE
- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.
- 자동 복구 메커니즘: 서버가 timeout 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가? 판단근거

### 캐시가능(Cacheable) GET, HEAD, POST, PATCH, *실제로는 GET, HEAD 정도만 캐시 가능
- 응답 결과 리소스를 캐시해서 사용해도 되는가?







1.  HEAD:GET 과 동일하지만 메세지 부분을 제외하고, 상태 줄과 헤더만 반환
OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)를 설명(주로 CORS 에서 사용)
CONNECT:대상 자원으로 식별되는 서버에 대한 터널을 설정
TRACE: 대상 리소스에 대한 경로를 따라 메세지 루프백 테스트를 수행


# HTTP 상태 코드
- 1xx(informational): 요청이 수신되어 처리중
- 2xx(successful): 요청 정상 처리
- 3xx(redirection): 요청을 완료하려면 추가 행동이 필요
- 4xx(client error): 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음
- 5xx(server error): 서버 오류, 서버가 정상 요청을 처리하지 못함



# HTTP 해더
### Content-Type: 표현 데이터의 형식
### Content-Encoding: 표현 데이터의 압축 방식, 압축전송
### Content-Language: 표현 데이터의 자연 언어
### Content-Length: 표현 데이터의 길이, 단순전송
### Transfer-Encodin: 분할 전송
### Range, Content-Range: 범위 전송 Range: bytes=1001-2000
### From: 유저 에이전트의 이메일 정보
- 검색엔진에 주로 사용

### Referer: 이전 웹페이지의 주소
- 유입경로 분석가능

### User-Agent: 유저 에이전트 애플리케이션 정보
- 통계 정보, 웹브라우저, 어떤 종류의 브라우저에서 장애가 발생하는지 파악가능

### Server: 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
### Date: 메세지가 발생한 시간

# 특별한 정보
### Host: 요청한 호스트의 정보(도메인) 서버를 찾아갈 수 있도록
### Location: 페이지 리다이렉션

# 인증
### Authorization: 클라이언트 인증 정보를 서버에 전달
### WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의

# 쿠키
### Set-Cookie: 서버에서 클라이언트로 쿠키전달(응답)
### Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고 HTTP 요청시 서버로 전달


## 협상: 협상 헤더는 요청시에만 사용
### Accept: 클라이언트가 선호하는 미디어 타입 전달
### Accept-Charset: 클라이언트가 선호하는 문자 인코딩
### Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
### Accept-Language: 클라이언트가 선호하는 자연언어

## 협상과 우선순위
- 0~1, 클수록 높은 우선순위
- 생략은 1
```
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
```

## 전송방식:
Content-length: 단순전송
Content

# 캐시와 조건부 요청
cache-control: max-age=60  
캐시가 유요한 시간  
브라우저가 60초 동안 캐시에 있는 내용을 바로 가져온다.
- 브라우저 로딩속도 증가
- 빠른 사용자 경험

cache-control: max-age=60  
Last-Modified: 2020년 1월 1일 10:00:00
- 이 데이터가 마지막에 수정된 시간
- [요청] if-modified-since: 2020년 1월 1일 10:00:00
- [응답] 304 Not Modified cache-control:max-age=60, 바디정보 없음


E-tag, If-None-Match
진짜 단순하게 ETag 만 보내서 같으면 유지, 다르면 다시 받기

# 프록시 캐시
Cache-Control: public, 응답이 public 캐시에 저장되어도 됨  
Cache-Control: private, 응답이 public 캐시에 저장되면 안됨!  
Cache-Control: s-maxage, 프록시 캐시에만 적용되는 max-age  
Age: 60 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간  

# 캐시 무효화
Cache-Control: no-cache, no-store, must-revalidate
