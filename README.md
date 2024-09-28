# 일기 다이어리 시스템 개발
## 프로젝트 소개
Spring Boot와 Java를 이용하여 일기 다이어리 (일기 생성, 일기 조회 (일별, 기간별), 일기 수정, 일기 삭제)를 구현한다.
## 기술 스택
- Spring boot 3.3.4 (JDK 17)
- Gradle
- Dependency : **Jnuit, Lombok, Spring Web, JPA, json, springdoc(Swagger), mysql-connector, jdbc ( 사용하지않고, 연습용으로 이용 )**
- DB Tool : MYSQL WORKBENCH
- POSTMAN
## 주요 기능
### 01. 일기 다이어리 생성
- POST /create/diary
- 파라미터 : 생성할 일기의 날짜 (Ex. yyyy-MM-dd)
- 일기 데이터 : OpenWeatherMap에서 날씨 API 데이터를 매일 새벽 1시마다 WeatherData 테이블에 저장하여 이용
과거 날씨 데이터가 있다면, 해당 데이터를 사용하여 일기를 생성하고,
과거 날씨 데이터가 없다면, 현재의 날씨를 가져와 일기를 생성
- 성공 응답 : 입력한 일기 TEXT와 함께 해당 날짜 일기 생성 (중복 생성 가능, 응답은 Void 바로 DB에 저장)
### 02. 일기 다이어리 조회
- GET /read/diary
- 파라미터 : 조회할 일기의 날짜 (Ex. yyyy-MM-dd)
- 성공 응답 : 해당 날짜의 모든 일기 데이터 조회

- GET /read/diaries
- 파라미터 : 조회할 기간의 첫번째 날 (Ex. yyyy-MM-dd) & 조회할 기간의 마지막 날 (Ex. yyyy-MM-dd)
- 성공 응답 : 해당 기간의 모든 일기 데이터 조회
### 03. 일기 다이어리 수정
- PUT /update/diary
- 파라미터 : 수정할 일기의 날짜 (Ex. yyyy-MM-dd)
- 성공 응답 : 입력한 일기 TEXT로 해당 날짜의 첫번째 일기 내용 수정 (응답은 Void, 바로 DB의 해당 데이터 수정)
### 04. 일기 다이어리 삭제
- DELETE /delete/diary
- 파라미터 : 삭제할 일기의 날짜 (Ex. yyyy-MM-dd)
- 성공 응답 : 해당 날짜의 첫번째 일기 데이터 삭제 (응답은 Void, 바로 DB에서 해당 데이터 삭제)
## 구현 시 문제점
**Spring Boot 3.x 이상의 버전부터 Swagger 이용 시 더 이상 Springfox 지원불가**

*해결방안* : Springdoc을 이용하여 Swagger 이용 (어노테이션과 메소드가 달라 Springdoc에 대한 학습 필요 -> 완벽한 Swagger 구현불가)
