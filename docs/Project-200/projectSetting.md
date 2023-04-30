---
layout: default
title: 프로젝트 설정
parent: 프로젝트-200
---

# 프로젝트 설정
{: .no_toc }
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

## 프로젝트 목적
01 스프링프레임워크에 대한 이해를 높히는데 목적이 있다.  
02 향후 해결하고 싶은 문제, 프로젝트의 방향이 구체화되면 정의하도록 한다.

## 프로젝트 설정

``` html
https://start.spring.io/
```
`Gradle`  
Gradle은 빌드 자동화 도구 중 하나, 프로젝트의 의존성 관리와 빌드 과정을 관리하는 데 사용

`Jar`  
자바 클래스 파일, 메타데이터 및 리소스 파일을 하나로 묶은 압축 파일  
라이브러리나 애플리케이션을 배포할 때 자주 사용  
Java에서는 jar 파일을 실행 가능한 애플리케이션으로 작성 가능  
스프링 부트에서는 애플리케이션을 jar 파일로 패키징하여 배포하는 것이 일반적
### 01 디팬던시 추가
`springWeb`  
스프링 웹 프레임워크를 사용하기 위한 필수 의존성으로, 스프링 MVC 등 웹 어플리케이션을 구축하는 데 필요한 기본적인 기능들을 제공

`Lombok`  
자바에서 번거로운 getter, setter, toString 등을 자동으로 생성해주는 라이브러리

`Thymeleaf`  
자바 템플릿 엔진으로, HTML, XML, JavaScript, CSS 등을 랜더링할 수 있습니다. 스프링 프레임워크에서 권장하는 뷰 엔진

`H2 database`  
자바로 작성된 오픈소스 인메모리 데이터베이스로, 가벼우며 빠른 속도와 SQL 호환성을 제공

`JDBC API`  
자바 데이터베이스 접근을 위한 API로, JDBC 드라이버를 사용하여 데이터베이스에 접속하고 SQL 쿼리를 실행  
스프링에서 JDBC API를 사용하여 데이터베이스에 접근

### 02. 생성
GENERATE 클릭
