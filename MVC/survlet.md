# HTTP 데이터 전송 방법 3 가지
### 01. GET - 쿼리 파라미터
- url?username=gim&age=18
- 메세지 바디 없이 쿼리 파라미터에 데이터를 포함해서 전달한다.
- 필터, 검색 페이지 등에 많이 쓰인다.

```java
//전체파라미터 조회
request.getParameterNames().asIterator()
        .forEachRemaining(paramName -> System.out.println(paramName + ": " + request.getParameter(paramName)));
```
```java
// 단일 파라미터 조회
String username = request.getParameter("username");
```
```java
// 중복 파라미터 조회
String[] parameterValues = request.getParameterValues("username");
```
### 02. POST - HTML Form
- Content-Type: application/x-www-form-urlencoded
- 메세지 바디에 쿼리파라미터 방식으로 전달
### 03. HTTP message body
- HTTP API 형식, 주로 JSON, XML 등에서 사용
