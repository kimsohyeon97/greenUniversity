<img width="1352" alt="스크린샷 2025-06-07 오후 7 58 24" src="https://github.com/user-attachments/assets/3c243976-0ce7-4038-a32f-19b6abb0d81c" />
<br><br>

## 개요
- 프로젝트 이름 : greenUniversity
- 프로젝트 목적 : 그린대학교 학사 및 커뮤니티 관리 시스템
- 프로젝트 지속기간 : 2025.04.10-2025.03.07
- 팀 : 2조 
<br><br>

## 사용 기술
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/SpringBoot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![JPA](https://img.shields.io/badge/JPA-Hibernate-59666C?style=for-the-badge)
![QueryDSL](https://img.shields.io/badge/QueryDSL-0769AD?style=for-the-badge)
![ModelMapper](https://img.shields.io/badge/ModelMapper-4285F4?style=for-the-badge)
![MySQL](https://img.shields.io/badge/MySQL-00000F?style=for-the-badge&logo=mysql&logoColor=white)
![Lombok](https://img.shields.io/badge/Lombok-EA3324?style=for-the-badge)
![Slf4j](https://img.shields.io/badge/Slf4j-0085CA?style=for-the-badge)
![REST API](https://img.shields.io/badge/RESTful%20API-6C757D?style=for-the-badge)<br><br>

### 👉🏻 CI/CD 및 배포 환경
### GitHub Actions를 활용한 자동화 빌드 및 테스트
* 코드 푸시 시 자동으로 빌드, 테스트 진행
* 빌드 성공 시 자동 배포 트리거<br><br>

### AWS EC2 인스턴스에 애플리케이션 배포
* Spring Boot 애플리케이션을 EC2에 배포하여 실제 서비스처럼 실시간 제공
* 보안 그룹 설정 및 포트 관리로 안정적인 서비스 운영<br><br>

## 내가 구현한 기능 
자세한 코드 리뷰 : https://fish-fahrenheit-662.notion.site/2-20c4ffb4f47b805698f0d843d39dc217?source=copy_link

## 1️⃣ 커뮤니티 게시판 목록 조회

카테고리별(공지사항, 자유게시판, 자료실) 게시글을 구분해 조회하고,  
검색 · 정렬 · 페이지네이션을 통합 처리한 커뮤니티 기능입니다.

-  QueryDSL 기반 **카테고리별 동적 검색 쿼리** 구현
-  `PageRequestDTO`, `PageResponseDTO` 기반 **공통 페이징 구조** 설계
-  `Community1`과 `User` 엔티티 **조인 조회**로 작성자 이름 출력
-  `ModelMapper`를 활용한 **Entity → DTO 자동 매핑**

사용 기술  : `Spring Boot` · `QueryDSL` · `ModelMapper` · `JPA` · `MySQL` · `DTO 기반 페이징`

## 2️⃣ 커뮤니티 게시글 검색

공지사항 · 자유게시판 · 자료실 등 카테고리별로 분기된 URL을 통해  
제목, 내용, 작성자 기준으로 게시글을 검색할 수 있습니다.

-  `QueryDSL` 기반 **카테고리 + 동적 조건 조합** 검색 구현
-  `PageRequestDTO`, `PageResponseDTO` 기반 **페이징 통합 처리**
-  `Community1` ↔ `User` 조인으로 **작성자 이름 포함 결과 조회**
-  `ModelMapper` 사용으로 **Entity → DTO 변환 자동화**

사용 기술  : `Spring Boot` · `QueryDSL` · `ModelMapper` · `JPA` · `MySQL` · `DTO 기반 페이징`

## 3️⃣ 커뮤니티 게시글 보기

게시글 열람 시 **조회수 증가**와 **상세 정보 출력**, **첨부파일 다운로드**, **비밀번호 잠금 확인** 등을 처리합니다.  
카테고리별로 view1~view4로 분기 처리되며, 트랜잭션 기반으로 조회수를 안정적으로 반영합니다.

-  조회수 증가 – `@Transactional`로 데이터 일관성 확보
-  작성자 정보 포함 상세 조회 – Entity → DTO 변환
-  비밀번호 게시글 AJAX 인증 처리
-  첨부파일 다운로드 + 다운로드 수 증가

사용 기술  : `Spring Boot` · `ModelMapper` · `JPA` · `MySQL` · `DTO` · `MultipartFile` · `AJAX`

## 4️⃣ 커뮤니티 글쓰기

카테고리(공지, 자유, 자료공유, 묻고답하기)별로 구분된 게시판에 글 작성 및 첨부파일 업로드 기능을 제공합니다.  
**작성자 IP 저장**, **다중 파일 처리**, **글-파일 연동**, **DTO 기반 엔티티 변환**을 통해 확장성과 유지보수성을 고려한 구조입니다.

-  Multipart 파일 업로드 및 메타데이터 DB 저장
-  글 등록 후 외래키(no)를 이용한 파일 연동
-  사용자 IP 저장으로 보안 및 로그 추적 가능
-  카테고리별 컨트롤러 분기로 게시판 기능 분리
-  ModelMapper로 Entity ↔ DTO 자동 매핑

사용 기술  : `Spring Boot` · `ModelMapper` · `MultipartFile` · `JPA` · `MySQL` · `UUID` · `DTO`

## 5️⃣ 커뮤니티 글 수정

작성자는 기존 글을 언제든지 수정할 수 있으며,  
**ModelMapper 기반 DTO → Entity 매핑**,  
**트랜잭션 기반 수정 처리**,  
**작성자 검증 및 예외 처리**를 통해  
안전하고 일관된 수정 로직을 구현했습니다.

-  GET 방식으로 기존 글 데이터 조회 후 수정 폼 출력
-  POST 방식으로 수정 요청 처리 → DTO로 받은 값 덮어쓰기
-  `ModelMapper`로 수정 항목 자동 매핑
-  `@Transactional`로 실패 시 자동 롤백 처리

사용 기술  : `Spring Boot` · `ModelMapper` · `@Transactional` · `Exception Handling` · `DTO 기반 수정 처리`

## 6️⃣ 커뮤니티 글 삭제

사용자가 작성한 게시글을 삭제할 수 있으며,  
**댓글, 첨부파일까지 함께 삭제**되도록 설계했습니다.  
Controller에서는 간단한 요청만 받고,  
Service에서 관련 리포지토리를 통해 일괄 처리합니다.

-  게시글 + 댓글 + 첨부파일 **동시 삭제**
-  삭제 완료 후 카테고리 목록으로 자동 리디렉션
-  Repository 단위 삭제 → 추후 트랜잭션 도입 가능

사용 기술  : `Spring Boot`, `JPA`, `Repository 연계 삭제`, `DTO`, `Cascade 또는 순차 삭제 설계`













