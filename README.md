# 공영주차장 감시대응 솔루션

'25년 제주 스마트도시 데이터허브 시범솔루션 발굴사업의 공통모듈 공개 패키지입니다. ((주)진우소프트이노베이션)

데이터허브 데이터마트에 적재된 영상(CCTV)·음원·CO2 이벤트와 전기차 충전기 상태를 주기적으로 조회해 위험도를 산정하고, 현장 상황·최종 이벤트·SOP 대응을 관리하는 웹 애플리케이션입니다.

> 현재 공개 문서 10종을 먼저 등록했으며, 소스코드는 공개용 점검을 마친 뒤 추가합니다.

## 공개 범위

| 구분 | 내용 |
|---|---|
| 공개 | 애플리케이션 소스(서버·화면), DB 스키마와 기초 코드, 위험도 규칙, 빌드·설치 스크립트, 문서 10종 |
| 포함하지 않음 | 데이터허브 플랫폼(D.Hub)·데이터마트, 영상분석(VURIX)·음원·CO2 장비 등 외부 시스템. 솔루션은 데이터마트와 SQL로 연계 |
| 제외 | 운영 환경 설정값(`.env`), 계정·인증키·인증서, 서버 주소, 현장에서 수집한 실제 이벤트·영상 데이터 |

기초 데이터의 사용자·연락처는 예시 값이고, 장치 목록은 시범 주차장 3곳의 장치 구성입니다(장치 IP 제외).

## 문서

| No | 문서 | 파일 |
|---|---|---|
| 1 | 소스코드 구성 | [docs/01_소스코드.pdf](docs/01_소스코드.pdf) |
| 2 | 설치·배포 가이드 (인프라 요구사항 포함) | [docs/02_설치배포가이드.pdf](docs/02_설치배포가이드.pdf) |
| 3 | 빌드 스크립트·실행 환경 (Docker Compose) | [docs/03_빌드스크립트_실행환경.pdf](docs/03_빌드스크립트_실행환경.pdf) |
| 4 | API 명세서 및 호출 예제 (cURL, Python) | [docs/04_API명세서_호출예제.pdf](docs/04_API명세서_호출예제.pdf) |
| 5 | 사용자 가이드 | [docs/05_사용자가이드.pdf](docs/05_사용자가이드.pdf) |
| 6 | 관리자 운영 매뉴얼 | [docs/06_관리자운영매뉴얼.pdf](docs/06_관리자운영매뉴얼.pdf) |
| 7 | 아키텍처 문서 | [docs/07_아키텍처문서.pdf](docs/07_아키텍처문서.pdf) |
| 8 | 필수 관리 문서 (LICENSE, README, NOTICE) | [docs/08_필수관리문서_LICENSE_README_NOTICE.pdf](docs/08_필수관리문서_LICENSE_README_NOTICE.pdf) |
| 9 | 오픈소스 사용내역 (SBOM) | [docs/09_오픈소스사용내역_SBOM.pdf](docs/09_오픈소스사용내역_SBOM.pdf) |
| 10 | 실행 가능한 샘플 데이터 | [docs/10_샘플데이터.pdf](docs/10_샘플데이터.pdf) |

## 빠른 시작 (시험용)

```bash
cp .env.example .env          # DB_PASSWORD, DB_ROOT_PASSWORD 입력. 지도를 보려면 VWORLD_KEY도 입력
docker compose up -d --build  # http://localhost:8090/monitoring
```

컨테이너 안에서 소스를 빌드하므로 인터넷이 필요합니다. 로그인과 데이터마트 연계는 꺼진 상태로 실행됩니다. 운영 서버 설치는 설치·배포 가이드를 따릅니다.

## 개발 환경

- Java 17, Spring Boot 3.5, MyBatis, Thymeleaf
- MariaDB 10.5 이상 (DB 스키마는 Flyway로 자동 생성. 설치 패키지는 11.2 사용)
- 화면 CSS: Tailwind CSS (Node.js 필요, 화면을 수정할 때만)

## 주요 설정 (.env)

| 항목 | 설명 |
|---|---|
| DB_URL, DB_USERNAME, DB_PASSWORD | 감시대응 DB 접속정보 |
| VWORLD_KEY | V-World 지도 인증키 |
| DATAMART_* | 데이터허브 데이터마트 접속정보와 연계 SQL (충전기·주차장 조회, 영상·음원·CO2 이벤트 조회, 최종 이벤트 적재) |
| AUTH_ENABLED, DHUB2_* | 데이터허브(D.Hub) 통합 로그인 설정 |
| NO_RESPONSE_ENABLED | 장비 무응답 이벤트 생성 여부 |

## 라이선스

[MIT License](LICENSE)로 배포합니다. 사용한 오픈소스는 [NOTICE](NOTICE)와 오픈소스 사용내역(SBOM)에 있습니다.

## 기술 문의

(주)진우소프트이노베이션 · 064-742-1816
